---
title: "PoolChunk"
sequence: "103"
---

[UP](/netty.html)

## 基本

- PageSize: 8192
- ChunkSize: 4 * 1024 * 1024

| Concept | Netty Class |
|---------|-------------|
| Page    |             |
| Chunk   | PoolChunk   |

## Run

## Handle

## 分配空间

### 分配 Normal

### 分配 Huge

## 释放空间

## 算法

- Buddy 伙伴算法：外部碎片
- Slab 算法：内部碎片

单独一个文档来记录这两个算法


