---
title: "PoolChunk"
sequence: "103"
---

[UP](/netty.html)

## PoolChunk 介绍

### 基本概念

| Concept | Netty Class |
|---------|-------------|
| Chunk   | PoolChunk   |
| Page    |             |
| PageRun |             |
| Subpage | PoolSubpage |


{:refdef: style="text-align: center;"}
![](/assets/images/netty/buf/netty-buffer-pool-chunk-concept-illustrated.svg)
{:refdef}

### Chunk 结构

{:refdef: style="text-align: center;"}
![](/assets/images/netty/buf/netty-buffer-pool-chunk-structure.svg)
{:refdef}

### Handle

在 `PoolChunk` 当中，**handle** 是一个 `long` 类型的数值，它用来表示 PageRun 和 Subpage 的信息：

```text
+------------------+---------------------+--------------+-----------------+--------------------------------+
│             PageRun (30 bit)           │            Mark (2 bit)        │       Subpage   (32 bit)       │
+------------------+---------------------+--------------+-----------------+--------------------------------+
│runOffset (15 bit)│num of pages (15 bit)│isUsed (1 bit)│isSubpage (1 bit)│       bitmapIdx (32 bit)       │
+------------------+---------------------+--------------+-----------------+--------------------------------+
```

```text
oooooooo ooooooos ssssssss ssssssue bbbbbbbb bbbbbbbb bbbbbbbb bbbbbbbb
```

- `o`: `runOffset` (page offset in the chunk), 15bit
- `s`: `size` (number of pages) of this run, 15bit
- `u`: `isUsed`?, 1bit
- `e`: `isSubpage`?, 1bit
- `b`: `bitmapIdx` of subpage, zero if it's not subpage, 32bit



```text
handle = 000000000000000 000001000000000 0000000000000000000000000000000000
runOffset = 0
size = 512
isUsed = 0
isSubpage = 0
bitmapIdx = 0
```

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

### 分配空间 Normal

### 分配空间 Huge


### 释放空间

