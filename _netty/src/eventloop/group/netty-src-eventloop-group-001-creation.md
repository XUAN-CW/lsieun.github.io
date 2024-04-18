---
title: "EventLoopGroup 创建"
sequence: "101"
---

[UP](/netty.html)

{:refdef: style="text-align: center;"}
![](/assets/images/netty/eventloop/netty-eventloop-relation.svg)
{:refdef}

## EventLoopGroup 相关类

{:refdef: style="text-align: center;"}
![](/assets/images/netty/eventloop/group/netty-eventloop-group-class-hierarchy.svg)
{:refdef}

## 创建过程

{:refdef: style="text-align: center;"}
![](/assets/images/netty/eventloop/group/netty-eventloop-group-parameter.svg)
{:refdef}


### 线程数量

```java
public abstract class MultithreadEventLoopGroup extends MultithreadEventExecutorGroup implements EventLoopGroup {
    private static final int DEFAULT_EVENT_LOOP_THREADS;

    static {
        DEFAULT_EVENT_LOOP_THREADS = Math.max(
                1,
                SystemPropertyUtil.getInt("io.netty.eventLoopThreads", NettyRuntime.availableProcessors() * 2)
        );

        if (logger.isDebugEnabled()) {
            logger.debug("-Dio.netty.eventLoopThreads: {}", DEFAULT_EVENT_LOOP_THREADS);
        }
    }
}
```

### chooser - SelectStrategy

### RejectedExecutionHandlers

### Executor - ThreadPerTaskExecutor

### SelectorProvider

## GlobalEventExecutor
