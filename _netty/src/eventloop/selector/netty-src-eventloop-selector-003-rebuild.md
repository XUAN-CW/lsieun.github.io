---
title: "Selector 空轮询"
sequence: "103"
---

[UP](/netty.html)

Nio 空轮询 bug 在哪里体现，如何解决？

- 重新创建一个 Selector，替换旧的 Selector。

JDK 只在 Linux 的 Selector 有 Bug
