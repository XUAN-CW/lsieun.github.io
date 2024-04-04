---
title: "EventLoop 线程启动"
sequence: "101"
---

[UP](/netty.html)

## 线程何时启动？

EventLoop 的 NIO 线程在何时启动？

- 当首次调用 `execute` 方法时

{:refdef: style="text-align: center;"}
![](/assets/images/netty/eventloop/thread/netty-eventloop-thread-1.svg)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/netty/eventloop/thread/netty-eventloop-thread-2.svg)
{:refdef}

## 如何避免线程重复启动

EventLoop 只有一个线程，会不会存在重复启动的问题？

- 通过状态位（`state`）控制线程只能启动一次

```java
public abstract class SingleThreadEventExecutor extends AbstractScheduledEventExecutor implements OrderedEventExecutor {
    private static final int ST_NOT_STARTED = 1;
    private static final int ST_STARTED = 2;
    private static final int ST_SHUTTING_DOWN = 3;
    private static final int ST_SHUTDOWN = 4;
    private static final int ST_TERMINATED = 5;

    private volatile int state = ST_NOT_STARTED;

    private static final AtomicIntegerFieldUpdater<SingleThreadEventExecutor> STATE_UPDATER =
            AtomicIntegerFieldUpdater.newUpdater(SingleThreadEventExecutor.class, "state");

    private void startThread() {
        // 未启动：ST_NOT_STARTED
        if (state == ST_NOT_STARTED) {
            // 尝试启动：ST_NOT_STARTED --> ST_STARTED
            if (STATE_UPDATER.compareAndSet(this, ST_NOT_STARTED, ST_STARTED)) {
                boolean success = false;
                try {
                    doStartThread();
                    success = true;
                } finally {
                    if (!success) {
                        // 未启动成功：ST_STARTED --> ST_NOT_STARTED
                        STATE_UPDATER.compareAndSet(this, ST_STARTED, ST_NOT_STARTED);
                    }
                }
            }
        }
    }
}
```
