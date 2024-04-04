---
title: "EventLoop"
sequence: "101"
---

[UP](/netty.html)

{:refdef: style="text-align: center;"}
![](/assets/images/netty/eventloop/netty-eventloop-classes.svg)
{:refdef}

## NioEventLoop

NioEventLoop 的重要组成：selector、线程、任务队列。

NioEventLoop 既会处理 IO 事件，也会处理普通任务和定时任务。
