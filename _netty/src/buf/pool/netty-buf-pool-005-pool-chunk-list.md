---
title: "PoolChunkList"
sequence: "105"
---

[UP](/netty.html)

核心问题：

- [ ] Chunk 迁移过程

## Chunk 迁移

《雪中悍刀行》中武者境界由共分九品，一品四境，分别是金刚境、指玄境、天象境、陆地神仙境。

## qInit 与 q000 区别

- qInit 相当于“新手村”，使用率到达 `0%` 时，不会释放
- q000，则会释放。

画一个图：qInit 是 Chunk 的入口，q000 是 Chunk 的出口。



