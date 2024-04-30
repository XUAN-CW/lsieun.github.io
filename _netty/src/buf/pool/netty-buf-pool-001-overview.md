---
title: "Pool Overview"
sequence: "101"
---

[UP](/netty.html)

jemalloc 是一种用于内存分配和管理的开源库，它专门针对多线程应用程序进行了优化。其名称来源于其作者 Jason Evans 的姓名和 "malloc"，即动态内存分配函数的名称。

Each application is configured at run-time to have a fixed number of arenas.
By default, the number of arenas depends on the number of processors.

```text
the number of processors --> the number of arenas
```

**Chunks** are usually managed by particular **arenas**,
and observing those associations is critical to correct function of the allocator.
The chunk size is 2 MB by default.

```text
arena --> chunk
```

**Chunks** are always the same size, and start at chunk-aligned addresses.
**Arenas** carve **chunks** into smaller allocations,
but **huge allocations** are directly backed by one or more contiguous chunks.

Allocation size classes fall into three major categories: **small**, **large**, and **huge**.
All allocation requests are rounded up to the nearest size class boundary.

**Huge** allocations are larger than **half of a chunk**, and are directly backed by dedicated chunks.
Metadata about huge allocations are stored in a single red-black tree.
Since most applications create few if any huge allocations, using a single tree is
not a scalability issue.

For **small and large allocations**, **chunks** are carved into **page runs** using the binary buddy algorithm.
Runs can be repeatedly split in half to as small as one page,
but can only be coalesced in ways that reverse the splitting process.
Information about **the states of the runs** is stored as **a page map** at the beginning of each chunk.
By storing this information separately from the runs,
pages are only ever touched if they are used.
This also enables the dedication of runs to large allocations,
which are larger than half of a page, but no larger than half of a chunk.

**Small allocations** fall into **three subcategories**: tiny, quantum-spaced, and sub-page.
Modern architectures impose alignment constraints on pointers, depending on data type.
malloc(3) is required to return memory that is suitably aligned for any purpose.
This worst case alignment requirement is referred to as the quantum size here (typically 16 bytes).
In practice, power-of-two alignment works for tiny allocations
since they are incapable of containing objects that are large enough to require quantum alignment.

## SizeClasses

```text
smallCacheSize = 256
normalCacheSize = 64

pageSize = 8192
00000000000000000010000000000000
pageShifts = 13

chunkSize = 4194304
00000000010000000000000000000000
chunkSizeShifts = 22

nHeapArena = 72


00000000010000000000000000 00 0000
group = 17
```



### handle

```text
handle = 000000000000000 000001000000000 0000000000000000000000000000000000
runOffset = 0
size = 512
isUsed = 0
isSubpage = 0
bitmapIdx = 0
```

```text
reqCapacity --> normCapacity
```

## PoolChunk

### handle

a **handle** is a long number, the bit layout of a run looks like:

```text
oooooooo ooooooos ssssssss ssssssue bbbbbbbb bbbbbbbb bbbbbbbb bbbbbbbb
```

- `o`: `runOffset` (page offset in the chunk), 15bit
- `s`: `size` (number of pages) of this run, 15bit
- `u`: `isUsed`?, 1bit
- `e`: `isSubpage`?, 1bit
- `b`: `bitmapIdx` of subpage, zero if it's not subpage, 32bit

## 复用

线程内如何利用内存，线程间如何共享内存

PoolArena 可以对应多个线程



## Reference

- [what does PageRun/PoolSubpage mean？](https://github.com/netty/netty/issues/7924)
    - [jemalloc white paper](https://www.bsdcan.org/2006/papers/jemalloc.pdf)
- [Netty learning journey——source code analysis Netty](https://medium.com/backenders-club/netty-learning-journey-source-code-analysis-netty-94e372d8a87b)
- [Netty Learning Journey — — Source Code](https://medium.com/backenders-club/netty-learning-journey-source-code-cd41de0f137)
- [PoolChunk](https://www.cnblogs.com/GrimReaper/p/10385343.html)
- [PooledByteBufAllocator buffer分配](https://www.code260.com/2020/04/20/netty4-pooled-buffer/)
- [jemalloc.pdf](https://people.freebsd.org/~jasone/jemalloc/bsdcan2006/jemalloc.pdf)
- []()
