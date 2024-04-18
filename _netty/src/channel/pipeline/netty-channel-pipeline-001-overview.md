---
title: "Pipeline 的相关概念"
sequence: "101"
---

[UP](/netty.html)

谈到 Netty 中的 Channel Pipeline，我们主要关注 `ChannelPipeline`、`ChannelHandlerContext` 和 `ChannelHandler` 三个核心概念

{:refdef: style="text-align: center;"}
![](/assets/images/netty/channel/pipeline/netty-channel-pipeline-structure-002-new.svg)
{:refdef}

## ChannelPipeline

{:refdef: style="text-align: center;"}
![](/assets/images/netty/channel/pipeline/netty-channel-pipeline-class-hierarchy.svg)
{:refdef}



```text
                                               I/O Request
                                          via {@link Channel} or
                                      {@link ChannelHandlerContext}
                                                    |
+---------------------------------------------------+---------------+
|                           ChannelPipeline         |               |
|                                                  \|/              |
|    +---------------------+            +-----------+----------+    |
|    | Inbound Handler  N  |            | Outbound Handler  1  |    |
|    +----------+----------+            +-----------+----------+    |
|              /|\                                  |               |
|               |                                  \|/              |
|    +----------+----------+            +-----------+----------+    |
|    | Inbound Handler N-1 |            | Outbound Handler  2  |    |
|    +----------+----------+            +-----------+----------+    |
|              /|\                                  .               |
|               .                                   .               |
| ChannelHandlerContext.fireIN_EVT() ChannelHandlerContext.OUT_EVT()|
|        [ method call]                       [method call]         |
|               .                                   .               |
|               .                                  \|/              |
|    +----------+----------+            +-----------+----------+    |
|    | Inbound Handler  2  |            | Outbound Handler M-1 |    |
|    +----------+----------+            +-----------+----------+    |
|              /|\                                  |               |
|               |                                  \|/              |
|    +----------+----------+            +-----------+----------+    |
|    | Inbound Handler  1  |            | Outbound Handler  M  |    |
|    +----------+----------+            +-----------+----------+    |
|              /|\                                  |               |
+---------------+-----------------------------------+---------------+
                |                                  \|/
+---------------+-----------------------------------+---------------+
|               |                                   |               |
|       [ Socket.read() ]                    [ Socket.write() ]     |
|                                                                   |
|  Netty Internal I/O Threads (Transport Implementation)            |
+-------------------------------------------------------------------+
```

{:refdef: style="text-align: center;"}
![](/assets/images/netty/channel/pipeline/netty-channel-pipeline-structure-002-new.svg)
{:refdef}

## ChannelHandler

{:refdef: style="text-align: center;"}
![](/assets/images/netty/channel/handler/netty-channel-handler-class-hierarchy.svg)
{:refdef}

## ChannelHandlerContext

{:refdef: style="text-align: center;"}
![](/assets/images/netty/channel/context/netty-channel-handler-context-class-hierarchy.svg)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/netty/channel/context/netty-channel-handler-context-class-hierarchy-hide-members.svg)
{:refdef}
