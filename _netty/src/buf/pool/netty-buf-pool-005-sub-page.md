---
title: "Subpage"
sequence: "105"
---

[UP](/netty.html)

## 基础

### 基本概念

```text
reqCapacity --> normCapacity = elemSize --> runSize
```

{:refdef: style="text-align: center;"}
![](/assets/images/netty/buf/netty-buffer-pool-subpage-concept.svg)
{:refdef}


### 空间范围

在 Netty 当中，SubPage 可以表示的空间范围是 `0~28KB`。

{:refdef: style="text-align: center;"}
![](/assets/images/netty/buf/netty-buffer-pool-size-class-capacity.svg)
{:refdef}

### 示例

#### 示例一

```java
import io.netty.buffer.ByteBuf;
import io.netty.buffer.PoolSubpage;
import io.netty.buffer.PooledByteBufAllocator;
import lsieun.utils.BufUtils;
import lsieun.utils.ChunkUtils;

public class HelloWorld {
    public static void main(String[] args) {
        // buf
        int requestCapacity = 3000;
        PooledByteBufAllocator allocator = PooledByteBufAllocator.DEFAULT;
        ByteBuf buf = allocator.heapBuffer(requestCapacity);

        // handle
        long handle = BufUtils.getHandle(buf);
        ChunkUtils.printHandle(handle);

        // subpage
        PoolSubpage<?> subpage = BufUtils.getSubpage(buf);
        ChunkUtils.printSubpage(subpage);
    }
}
```

```text
handle = 64424509440

Binary:
+---------------+---------------+-+-+--------------------------------+
│000000000000000│000000000000011│1│1│00000000000000000000000000000000│
+---------------+---------------+-+-+--------------------------------+

Table:
┌───────────┬───────┬─────────┬───────────┬───────────┐
│ runOffset │ pages │ isUsed  │ isSubpage │ bitmapIdx │
├───────────┼───────┼─────────┼───────────┼───────────┤
│     0     │   3   │  true   │   true    │     0     │
└───────────┴───────┴─────────┴───────────┴───────────┘

Subpage:
┌─────────┬─────────────┬─────────┬─────────────────┬───────┬───────────────┬─────┐
│  Chunk  │  chunkSize  │ 4194304 │    pageSize     │ 8192  │  totalPages   │ 512 │
├─────────┼─────────────┼─────────┼─────────────────┼───────┼───────────────┼─────┤
│ PageRun │  runOffset  │    0    │     runSize     │ 24576 │     pages     │  3  │
├─────────┼─────────────┼─────────┼─────────────────┼───────┼───────────────┼─────┤
│ Subpage │ elementSize │  3072   │ maxNumElements  │   8   │ bitmapLength  │  1  │
├─────────┼─────────────┼─────────┼─────────────────┼───────┼───────────────┼─────┤
│ Bitmap  │  totalBits  │   64    │   invalidBits   │  56   │ numAvailable  │  7  │
└─────────┴─────────────┴─────────┴─────────────────┴───────┴───────────────┴─────┘

Bitmap:
┌───────────┬───────────────────────────────────────────────────────────────────┐
│ bitmap[0] │ XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX00000001  │
└───────────┴───────────────────────────────────────────────────────────────────┘
```

#### 示例二

```java
import io.netty.buffer.ByteBuf;
import io.netty.buffer.PoolSubpage;
import io.netty.buffer.PooledByteBufAllocator;
import lsieun.cst.MyConst;
import lsieun.utils.BufUtils;
import lsieun.utils.ChunkUtils;

import java.util.ArrayList;
import java.util.List;

public class HelloWorld {
    public static void main(String[] args) {
        int requestCapacity = 200;
        PooledByteBufAllocator allocator = PooledByteBufAllocator.DEFAULT;

        List<ByteBuf> bufList = new ArrayList<>();
        // 分配 3 个，进行比对
        for (int i = 0; i < 3; i++) {
            // buf
            ByteBuf buf = allocator.heapBuffer(requestCapacity);
            bufList.add(buf);

            // handle
            long handle = BufUtils.getHandle(buf);
            ChunkUtils.printHandle(handle);

            // subpage
            PoolSubpage<?> subpage = BufUtils.getSubpage(buf);
            ChunkUtils.printSubpage(subpage);

            System.out.println(MyConst.SEPARATION_LINE);
            System.out.println();
        }



        for (ByteBuf buf : bufList) {
            buf.release();
        }
    }
}
```

#### 示例三

```text
# name,operation,bytes,show
buf1,allocate,500,true
buf2,allocate,500,true
buf3,allocate,500,true
buf2,free,500,true
buf1,free,500,true
buf3,free,500,true
```

```java
import io.netty.buffer.ByteBuf;
import io.netty.buffer.PoolSubpage;
import lsieun.utils.BufUtils;
import lsieun.utils.ChunkUtils;

import java.io.IOException;
import java.util.function.Consumer;
import java.util.function.Function;

public class HelloWorld {
    public static void main(String[] args) throws IOException {
        Function<ByteBuf, PoolSubpage<?>> func = BufUtils::getSubpage;
        Consumer<PoolSubpage<?>> consumer = ChunkUtils::printSubpage;
        BufUtils.processBytes(true, func, consumer);
    }
}
```

#### 示例四


```java
import io.netty.buffer.ByteBuf;
import io.netty.buffer.PoolChunk;
import io.netty.buffer.PooledByteBufAllocator;
import io.netty.buffer.SizeClasses;
import lsieun.cst.MyConst;
import lsieun.drawing.theme.table.TableType;
import lsieun.drawing.utils.TableUtils;
import lsieun.utils.BufUtils;

public class HelloWorld {
    public static void main(String[] args) {
        PooledByteBufAllocator allocator = PooledByteBufAllocator.DEFAULT;
        ByteBuf buf = allocator.heapBuffer(64 * MyConst.PAGE);

        PoolChunk<?> chunk = BufUtils.getChunk(buf);
        SizeClasses sizeClass = BufUtils.getSizeClass(buf);
        int pageSize = sizeClass.pageSize;
        int nSubpages = sizeClass.nSubpages;

        String[][] matrix = new String[nSubpages + 1][4];
        matrix[0][0] = "elemSize";
        matrix[0][1] = "runSize";
        matrix[0][2] = "pages";
        matrix[0][3] = "maxNumElems";
        for (int i = 0; i < nSubpages; i++) {
            int elemSize = sizeClass.sizeIdx2size(i);
            int runSize = chunk.calculateRunSize(i);
            int pages = runSize / pageSize;
            int maxNumElems = pages * pageSize / elemSize;

            matrix[i + 1][0] = String.valueOf(elemSize);
            matrix[i + 1][1] = String.valueOf(runSize);
            matrix[i + 1][2] = String.valueOf(pages);
            matrix[i + 1][3] = String.valueOf(maxNumElems);
        }

        TableUtils.printTable(matrix, TableType.ONE_LINE);
    }
}
```

```text
┌───────────┬─────────┬───────┬─────────────┐
│ elemSize  │ runSize │ pages │ maxNumElems │
├───────────┼─────────┼───────┼─────────────┤
│    16     │  8192   │   1   │     512     │
├───────────┼─────────┼───────┼─────────────┤
│    32     │  8192   │   1   │     256     │
├───────────┼─────────┼───────┼─────────────┤
│    48     │  24576  │   3   │     512     │
├───────────┼─────────┼───────┼─────────────┤
│    64     │  8192   │   1   │     128     │
├───────────┼─────────┼───────┼─────────────┤
│    80     │  40960  │   5   │     512     │
├───────────┼─────────┼───────┼─────────────┤
│    96     │  24576  │   3   │     256     │
├───────────┼─────────┼───────┼─────────────┤
│    112    │  57344  │   7   │     512     │
├───────────┼─────────┼───────┼─────────────┤
│    128    │  8192   │   1   │     64      │
├───────────┼─────────┼───────┼─────────────┤
│    160    │  40960  │   5   │     256     │
├───────────┼─────────┼───────┼─────────────┤
│    192    │  24576  │   3   │     128     │
├───────────┼─────────┼───────┼─────────────┤
│    224    │  57344  │   7   │     256     │
├───────────┼─────────┼───────┼─────────────┤
│    256    │  8192   │   1   │     32      │
├───────────┼─────────┼───────┼─────────────┤
│    320    │  40960  │   5   │     128     │
├───────────┼─────────┼───────┼─────────────┤
│    384    │  24576  │   3   │     64      │
├───────────┼─────────┼───────┼─────────────┤
│    448    │  57344  │   7   │     128     │
├───────────┼─────────┼───────┼─────────────┤
│    512    │  8192   │   1   │     16      │
├───────────┼─────────┼───────┼─────────────┤
│    640    │  40960  │   5   │     64      │
├───────────┼─────────┼───────┼─────────────┤
│    768    │  24576  │   3   │     32      │
├───────────┼─────────┼───────┼─────────────┤
│    896    │  57344  │   7   │     64      │
├───────────┼─────────┼───────┼─────────────┤
│   1024    │  8192   │   1   │      8      │
├───────────┼─────────┼───────┼─────────────┤
│   1280    │  40960  │   5   │     32      │
├───────────┼─────────┼───────┼─────────────┤
│   1536    │  24576  │   3   │     16      │
├───────────┼─────────┼───────┼─────────────┤
│   1792    │  57344  │   7   │     32      │
├───────────┼─────────┼───────┼─────────────┤
│   2048    │  8192   │   1   │      4      │
├───────────┼─────────┼───────┼─────────────┤
│   2560    │  40960  │   5   │     16      │
├───────────┼─────────┼───────┼─────────────┤
│   3072    │  24576  │   3   │      8      │
├───────────┼─────────┼───────┼─────────────┤
│   3584    │  57344  │   7   │     16      │
├───────────┼─────────┼───────┼─────────────┤
│   4096    │  8192   │   1   │      2      │
├───────────┼─────────┼───────┼─────────────┤
│   5120    │  40960  │   5   │      8      │
├───────────┼─────────┼───────┼─────────────┤
│   6144    │  24576  │   3   │      4      │
├───────────┼─────────┼───────┼─────────────┤
│   7168    │  57344  │   7   │      8      │
├───────────┼─────────┼───────┼─────────────┤
│   8192    │  8192   │   1   │      1      │
├───────────┼─────────┼───────┼─────────────┤
│   10240   │  40960  │   5   │      4      │
├───────────┼─────────┼───────┼─────────────┤
│   12288   │  24576  │   3   │      2      │
├───────────┼─────────┼───────┼─────────────┤
│   14336   │  57344  │   7   │      4      │
├───────────┼─────────┼───────┼─────────────┤
│   16384   │  16384  │   2   │      1      │
├───────────┼─────────┼───────┼─────────────┤
│   20480   │  40960  │   5   │      2      │
├───────────┼─────────┼───────┼─────────────┤
│   24576   │  24576  │   3   │      1      │
├───────────┼─────────┼───────┼─────────────┤
│   28672   │  57344  │   7   │      2      │
└───────────┴─────────┴───────┴─────────────┘
```



## 进阶

### Arena 和 Chunk


{:refdef: style="text-align: center;"}
![](/assets/images/netty/buf/netty-buffer-pool-subpage-relation.svg)
{:refdef}

### 分配过程

{:refdef: style="text-align: center;"}
![](/assets/images/netty/buf/netty-buffer-pool-subpage-allocation.svg)
{:refdef}

## 相关类

### PoolArena

```java
abstract class PoolArena<T> implements PoolArenaMetric {
    final PoolSubpage<T>[] smallSubpagePools;

    protected PoolArena(PooledByteBufAllocator parent, SizeClasses sizeClass) {
        this.sizeClass = sizeClass;

        smallSubpagePools = newSubpagePoolArray(sizeClass.nSubpages);
        for (int i = 0; i < smallSubpagePools.length; i++) {
            smallSubpagePools[i] = newSubpagePoolHead(i);
        }
    }

    private PoolSubpage<T> newSubpagePoolHead(int index) {
        PoolSubpage<T> head = new PoolSubpage<T>(index);
        head.prev = head;
        head.next = head;
        return head;
    }

    private void allocate(PoolThreadCache cache, PooledByteBuf<T> buf, final int reqCapacity) {
        final int sizeIdx = sizeClass.size2SizeIdx(reqCapacity);

        if (sizeIdx <= sizeClass.smallMaxSizeIdx) {
            tcacheAllocateSmall(cache, buf, reqCapacity, sizeIdx);
        }
        // 代码省略
    }

    private void tcacheAllocateSmall(PoolThreadCache cache, PooledByteBuf<T> buf, final int reqCapacity,
                                     final int sizeIdx) {

        if (cache.allocateSmall(this, buf, reqCapacity, sizeIdx)) {
            // was able to allocate out of the cache so move on
            return;
        }

        /*
         * Synchronize on the head.
         * This is needed as {@link PoolChunk#allocateSubpage(int)} and {@link PoolChunk#free(long)}
         * may modify the doubly linked list as well.
         */
        final PoolSubpage<T> head = smallSubpagePools[sizeIdx];
        final boolean needsNormalAllocation;
        head.lock();
        try {
            final PoolSubpage<T> s = head.next;
            needsNormalAllocation = s == head;
            if (!needsNormalAllocation) {
                assert s.doNotDestroy && s.elemSize == sizeClass.sizeIdx2size(sizeIdx) : "doNotDestroy=" +
                        s.doNotDestroy + ", elemSize=" + s.elemSize + ", sizeIdx=" + sizeIdx;
                long handle = s.allocate();
                assert handle >= 0;
                s.chunk.initBufWithSubpage(buf, null, handle, reqCapacity, cache);
            }
        }
        finally {
            head.unlock();
        }

        if (needsNormalAllocation) {
            lock();
            try {
                allocateNormal(buf, reqCapacity, sizeIdx, cache);
            }
            finally {
                unlock();
            }
        }

        incSmallAllocation();
    }

    private void allocateNormal(PooledByteBuf<T> buf, int reqCapacity, int sizeIdx, PoolThreadCache threadCache) {
        assert lock.isHeldByCurrentThread();
        // NOTE: 第 1 步，从现有的 Chunk List 中分配『数据空间』
        if (q050.allocate(buf, reqCapacity, sizeIdx, threadCache) ||
                q025.allocate(buf, reqCapacity, sizeIdx, threadCache) ||
                q000.allocate(buf, reqCapacity, sizeIdx, threadCache) ||
                qInit.allocate(buf, reqCapacity, sizeIdx, threadCache) ||
                q075.allocate(buf, reqCapacity, sizeIdx, threadCache)) {
            return;
        }

        // NOTE: 第 2 步，创建一个新的 Chunk
        // Add a new chunk.
        PoolChunk<T> c = newChunk(sizeClass.pageSize, sizeClass.nPSizes, sizeClass.pageShifts, sizeClass.chunkSize);

        // NOTE: 第 3 步，从新 Chunk 中分配一部分空间到 buf 上
        boolean success = c.allocate(buf, reqCapacity, sizeIdx, threadCache);
        assert success;

        // NOTE: 第 4 步，将 chunk 记录到 qInit 中
        qInit.add(c);
    }

    @Override
    protected final void finalize() throws Throwable {
        try {
            super.finalize();
        }
        finally {
            destroyPoolSubPages(smallSubpagePools);
            destroyPoolChunkLists(qInit, q000, q025, q050, q075, q100);
        }
    }

    private static void destroyPoolSubPages(PoolSubpage<?>[] pages) {
        for (PoolSubpage<?> page : pages) {
            page.destroy();
        }
    }
}
```

### PoolChunk

```java
final class PoolChunk<T> implements PoolChunkMetric {
    private final PoolSubpage<T>[] subpages;

    PoolChunk(PoolArena<T> arena, Object base, T memory, int pageSize, int pageShifts, int chunkSize, int maxPageIdx) {
        subpages = new PoolSubpage[chunkSize >> pageShifts];
    }
    
    boolean allocate(PooledByteBuf<T> buf, int reqCapacity, int sizeIdx, PoolThreadCache cache) {
        // NOTE: 第 1 步，获取『可用空间』（handle）
        final long handle;
        if (sizeIdx <= arena.sizeClass.smallMaxSizeIdx) {
            final PoolSubpage<T> nextSub;
            // small
            // Obtain the head of the PoolSubPage pool that is owned by the PoolArena and synchronize on it.
            // This is need as we may add it back and so alter the linked-list structure.
            PoolSubpage<T> head = arena.smallSubpagePools[sizeIdx];
            head.lock();
            try {
                nextSub = head.next;
                if (nextSub != head) {
                    assert nextSub.doNotDestroy && nextSub.elemSize == arena.sizeClass.sizeIdx2size(sizeIdx) :
                            "doNotDestroy=" + nextSub.doNotDestroy + ", elemSize=" + nextSub.elemSize + ", sizeIdx=" +
                                    sizeIdx;
                    // NOTE: 第 1.1.1 步，分配空间
                    handle = nextSub.allocate();
                    assert handle >= 0;
                    assert isSubpage(handle);

                    // NOTE: 第 1.1.2 步，将 handle 与 buf 绑定
                    nextSub.chunk.initBufWithSubpage(buf, null, handle, reqCapacity, cache);
                    return true;
                }

                // NOTE: 第 1.2 步，分配空间
                handle = allocateSubpage(sizeIdx, head);
                if (handle < 0) {
                    return false;
                }
                assert isSubpage(handle);
            }
            finally {
                head.unlock();
            }
        }
        // 代码省略

        ByteBuffer nioBuffer = cachedNioBuffers != null ? cachedNioBuffers.pollLast() : null;

        // NOTE: 第 2 步，将『可用空间』（handle） 与 buf 进行绑定
        initBuf(buf, nioBuffer, handle, reqCapacity, cache);
        return true;
    }

    void initBufWithSubpage(PooledByteBuf<T> buf, ByteBuffer nioBuffer, long handle, int reqCapacity,
                            PoolThreadCache threadCache) {
        int runOffset = runOffset(handle);
        int bitmapIdx = bitmapIdx(handle);

        PoolSubpage<T> s = subpages[runOffset];
        assert s.isDoNotDestroy();
        assert reqCapacity <= s.elemSize : reqCapacity + "<=" + s.elemSize;

        int offset = (runOffset << pageShifts) + bitmapIdx * s.elemSize;

        // TRACE:
        buf.init(this, nioBuffer, handle, offset, reqCapacity, s.elemSize, threadCache);
    }

    private long allocateSubpage(int sizeIdx, PoolSubpage<T> head) {
        // allocate a new run
        int runSize = calculateRunSize(sizeIdx);
        // runSize must be multiples of pageSize
        long runHandle = allocateRun(runSize);
        if (runHandle < 0) {
            return -1;
        }

        int runOffset = runOffset(runHandle);
        assert subpages[runOffset] == null;
        int elemSize = arena.sizeClass.sizeIdx2size(sizeIdx);

        PoolSubpage<T> subpage = new PoolSubpage<T>(head, this, pageShifts, runOffset,
                runSize(pageShifts, runHandle), elemSize);

        subpages[runOffset] = subpage;
        return subpage.allocate();
    }

    private int calculateRunSize(int sizeIdx) {
        int maxElements = 1 << pageShifts - SizeClasses.LOG2_QUANTUM;
        int runSize = 0;
        int nElements;

        final int elemSize = arena.sizeClass.sizeIdx2size(sizeIdx);

        // find the lowest common multiple of pageSize and elemSize
        do {
            runSize += pageSize;
            nElements = runSize / elemSize;
        } while (nElements < maxElements && runSize != nElements * elemSize);

        while (nElements > maxElements) {
            runSize -= pageSize;
            nElements = runSize / elemSize;
        }

        assert nElements > 0;
        assert runSize <= chunkSize;
        assert runSize >= elemSize;

        return runSize;
    }

    void free(long handle, int normCapacity, ByteBuffer nioBuffer) {
        if (isSubpage(handle)) {
            int sIdx = runOffset(handle);
            PoolSubpage<T> subpage = subpages[sIdx];
            assert subpage != null;
            PoolSubpage<T> head = subpage.chunk.arena.smallSubpagePools[subpage.headIndex];
            // Obtain the head of the PoolSubPage pool that is owned by the PoolArena and synchronize on it.
            // This is need as we may add it back and so alter the linked-list structure.
            head.lock();
            try {
                assert subpage.doNotDestroy;
                if (subpage.free(head, bitmapIdx(handle))) {
                    //the subpage is still used, do not free it
                    return;
                }
                assert !subpage.doNotDestroy;
                // Null out slot in the array as it was freed and we should not use it anymore.
                subpages[sIdx] = null;
            }
            finally {
                head.unlock();
            }
        }

        int runSize = runSize(pageShifts, handle);
        // start free run
        runsAvailLock.lock();
        try {
            // collapse continuous runs, successfully collapsed runs
            // will be removed from runsAvail and runsAvailMap
            long finalRun = collapseRuns(handle);

            //set run as not used
            finalRun &= ~(1L << IS_USED_SHIFT);
            //if it is a subpage, set it to run
            finalRun &= ~(1L << IS_SUBPAGE_SHIFT);

            insertAvailRun(runOffset(finalRun), runPages(finalRun), finalRun);
            freeBytes += runSize;
        }
        finally {
            runsAvailLock.unlock();
        }

        if (nioBuffer != null && cachedNioBuffers != null &&
                cachedNioBuffers.size() < PooledByteBufAllocator.DEFAULT_MAX_CACHED_BYTEBUFFERS_PER_CHUNK) {
            cachedNioBuffers.offer(nioBuffer);
        }
    }
}
```

### PoolSubpage

```java
final class PoolSubpage<T> implements PoolSubpageMetric {
    long allocate() {
        // NOTE: 第 1 步，参数校验
        if (numAvail == 0 || !doNotDestroy) {
            return -1;
        }

        // NOTE: 第 2 步，查找『可用空间』 - bitmapIdx
        final int bitmapIdx = getNextAvail();
        if (bitmapIdx < 0) {
            removeFromPool(); // Subpage appear to be in an invalid state. Remove to prevent repeated errors.
            throw new AssertionError("No next available bitmap index found (bitmapIdx = " + bitmapIdx + "), " +
                    "even though there are supposed to be (numAvail = " + numAvail + ") " +
                    "out of (maxNumElems = " + maxNumElems + ") available indexes.");
        }

        // NOTE: 第 3 步，bitmap 更新：将 bitmapIdx 代表的『可用空间』标记为『已经占用』
        int q = bitmapIdx >>> 6;
        int r = bitmapIdx & 63;
        assert (bitmap[q] >>> r & 1) == 0;
        bitmap[q] |= 1L << r;

        // NOTE: 第 4 步，更新 Arena 中的 smallSubpagePools
        if (--numAvail == 0) {
            removeFromPool();
        }

        // NOTE: 将 5 步，将 bitmapIdx 转换为 handle
        return toHandle(bitmapIdx);
    }

    boolean free(PoolSubpage<T> head, int bitmapIdx) {
        // NOTE: 第 1 步，回收『已占用空间』：根据 bitmapIdx 更新 bitmap
        int q = bitmapIdx >>> 6;
        int r = bitmapIdx & 63;
        assert (bitmap[q] >>> r & 1) != 0;
        bitmap[q] ^= 1L << r;

        // NOTE: 第 2步，将『已占用空间』转换为『可用空间』
        setNextAvail(bitmapIdx);

        // NOTE: 第 3 步，更新 Arena 中的 smallSubpagePools
        if (numAvail++ == 0) {
            // NOTE: 如果 numAvail == 0，则表示原来没有『剩余空间』，现在释放了一份『空间』，就将 SubPage 添加回 Arena
            addToPool(head);
            /* When maxNumElems == 1, the maximum numAvail is also 1.
             * Each of these PoolSubpages will go in here when they do free operation.
             * If they return true directly from here, then the rest of the code will be unreachable,
             * and they will not actually be recycled. So return true only on maxNumElems > 1.
             * */
            if (maxNumElems > 1) {
                return true;
            }
        }

        // NOTE: 第 4 步，更新 Arena 中的 smallSubpagePools
        if (numAvail != maxNumElems) {
            return true;
        }
        else {
            // Subpage not in use (numAvail == maxNumElems)
            // NOTE: 如果只剩下一个 SubPage，需要保留它
            if (prev == next) {
                // Do not remove if this subpage is the only one left in the pool.
                return true;
            }

            // NOTE: 如果剩下多个 SubPage，则进行移除操作
            // Remove this subpage from the pool if there are other subpages left in the pool.
            doNotDestroy = false;
            removeFromPool();
            return false;
        }
    }
}
```
