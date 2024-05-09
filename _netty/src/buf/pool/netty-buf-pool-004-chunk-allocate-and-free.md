---
title: "Chunk 空间分配过程"
sequence: "104"
---

[UP](/netty.html)

## Chunk 创建和销毁

### 创建

```java
abstract class PoolArena<T> implements PoolArenaMetric {
    protected abstract PoolChunk<T> newChunk(int pageSize, int maxPageIdx, int pageShifts, int chunkSize);

    protected abstract PoolChunk<T> newUnpooledChunk(int capacity);
}
```

{:refdef: style="text-align: center;"}
![](/assets/images/netty/buf/netty-buffer-pool-chunk-initial-state.svg)
{:refdef}

### 销毁

```java
abstract class PoolArena<T> implements PoolArenaMetric {
    protected abstract void destroyChunk(PoolChunk<T> chunk);
}
```

## Chunk 使用

```java
public class PooledByteBufAllocator extends AbstractByteBufAllocator implements ByteBufAllocatorMetricProvider {
    @Override
    protected ByteBuf newHeapBuffer(int initialCapacity, int maxCapacity) {
        PoolThreadCache cache = threadCache.get();
        PoolArena<byte[]> heapArena = cache.heapArena;

        final ByteBuf buf = heapArena.allocate(cache, initialCapacity, maxCapacity);

        return toLeakAwareBuffer(buf);
    }

    @Override
    protected ByteBuf newDirectBuffer(int initialCapacity, int maxCapacity) {
        PoolThreadCache cache = threadCache.get();
        PoolArena<ByteBuffer> directArena = cache.directArena;

        final ByteBuf buf = directArena.allocate(cache, initialCapacity, maxCapacity);

        return toLeakAwareBuffer(buf);
    }
}
```

```java
abstract class PoolArena<T> implements PoolArenaMetric {
    PooledByteBuf<T> allocate(PoolThreadCache cache, int reqCapacity, int maxCapacity) {
        PooledByteBuf<T> buf = newByteBuf(maxCapacity);

        allocate(cache, buf, reqCapacity);
        return buf;
    }

    private void allocate(PoolThreadCache cache, PooledByteBuf<T> buf, final int reqCapacity) {
        final int sizeIdx = sizeClass.size2SizeIdx(reqCapacity);

        if (sizeIdx <= sizeClass.smallMaxSizeIdx) {
            tcacheAllocateSmall(cache, buf, reqCapacity, sizeIdx);
        }
        else if (sizeIdx < sizeClass.nSizes) {
            tcacheAllocateNormal(cache, buf, reqCapacity, sizeIdx);
        }
        else {
            int normCapacity = sizeClass.directMemoryCacheAlignment > 0
                    ? sizeClass.normalizeSize(reqCapacity) : reqCapacity;

            // Huge allocations are never served via the cache so just call allocateHuge
            allocateHuge(buf, normCapacity);
        }
    }
}
```

### 分配空间 Normal

```java
final class PoolChunk<T> implements PoolChunkMetric {
    boolean allocate(PooledByteBuf<T> buf, int reqCapacity, int sizeIdx, PoolThreadCache cache) {
        int runSize = arena.sizeClass.sizeIdx2size(sizeIdx);

        final long handle = allocateRun(runSize);
    }

    private long allocateRun(int runSize) {
        // NOTE: 第 1 步，runSize (bytes) --> pages --> pageIdx
        int pages = runSize >> pageShifts;
        int pageIdx = arena.sizeClass.pages2pageIdx(pages);

        // NOTE: 第 2 步，从 runsAvail 中，获取『可用空间』，即获取 handle
        runsAvailLock.lock();
        try {
            // NOTE: 第 2.1 步，根据 pageIdx 查找 queueIdx
            // find first queue which has at least one big enough run
            int queueIdx = runFirstBestFit(pageIdx);
            if (queueIdx == -1) {
                return -1;
            }

            // NOTE: 第 2.2 步，根据 queueIdx 获取 queue
            // get run with min offset in this queue
            IntPriorityQueue queue = runsAvail[queueIdx];

            // NOTE: 第 2.3 步，从 queue 中获取 handle 的前 32 位
            long handle = queue.poll();
            assert handle != IntPriorityQueue.NO_VALUE;

            // NOTE: 第 2.4 步，转换成完整的 handle
            handle <<= BITMAP_IDX_BIT_LENGTH;
            assert !isUsed(handle) : "invalid handle: " + handle;

            // NOTE: 第 3 步，从 runsAvailMap 移除 handle 相关记录
            removeAvailRun0(handle);

            // NOTE: 第 4 步，将『可用空间』分出一部分空间，记录成『已使用空间』
            handle = splitLargeRun(handle, pages);

            // NOTE: 第 5 步，记录『总剩余空间』
            int pinnedSize = runSize(pageShifts, handle);
            freeBytes -= pinnedSize;

            // 返回
            return handle;
        }
        finally {
            runsAvailLock.unlock();
        }
    }
}
```

### 分配空间 Huge

```java
abstract class PoolArena<T> implements PoolArenaMetric {
    private void allocateHuge(PooledByteBuf<T> buf, int reqCapacity) {
        PoolChunk<T> chunk = newUnpooledChunk(reqCapacity);
        activeBytesHuge.add(chunk.chunkSize());
        buf.initUnpooled(chunk, reqCapacity);
        allocationsHuge.increment();
    }
}
```

### 释放空间

```java
abstract class PoolArena<T> implements PoolArenaMetric {
    void free(PoolChunk<T> chunk, ByteBuffer nioBuffer, long handle, int normCapacity, PoolThreadCache cache) {
        chunk.decrementPinnedMemory(normCapacity);
        if (chunk.unpooled) {
            int size = chunk.chunkSize();
            destroyChunk(chunk);
            activeBytesHuge.add(-size);
            deallocationsHuge.increment();
        }
        else {
            SizeClass sizeClass = sizeClass(handle);
            if (cache != null && cache.add(this, chunk, nioBuffer, handle, normCapacity, sizeClass)) {
                // cached so not free it.
                return;
            }

            freeChunk(chunk, handle, normCapacity, sizeClass, nioBuffer, false);
        }
    }

    void freeChunk(PoolChunk<T> chunk, long handle, int normCapacity, SizeClass sizeClass, ByteBuffer nioBuffer,
                   boolean finalizer) {
        final boolean destroyChunk;
        lock();
        try {
            // We only call this if freeChunk is not called because of the PoolThreadCache finalizer as otherwise this
            // may fail due lazy class-loading in for example tomcat.
            if (!finalizer) {
                switch (sizeClass) {
                    case Normal:
                        ++deallocationsNormal;
                        break;
                    case Small:
                        ++deallocationsSmall;
                        break;
                    default:
                        throw new Error();
                }
            }
            destroyChunk = !chunk.parent.free(chunk, handle, normCapacity, nioBuffer);
        }
        finally {
            unlock();
        }
        if (destroyChunk) {
            // destroyChunk not need to be called while holding the synchronized lock.
            destroyChunk(chunk);
        }
    }
}
```

```java
final class PoolChunkList<T> implements PoolChunkListMetric {
    
}
```
