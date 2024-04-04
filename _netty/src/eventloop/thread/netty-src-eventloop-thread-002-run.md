---
title: "EventLoop 线程运行"
sequence: "102"
---

[UP](/netty.html)

## 运行状态：处理任务

- Channel IO 任务
- 普通任务
- 定时任务

### Channel IO

{:refdef: style="text-align: center;"}
![](/assets/images/netty/eventloop/thread/netty-eventloop-thread-run-channel-io.svg)
{:refdef}

```java
public final class NioEventLoop extends SingleThreadEventLoop {
    private void processSelectedKeys() {
        if (selectedKeys != null) {
            processSelectedKeysOptimized();
        }
        else {
            processSelectedKeysPlain(selector.selectedKeys());
        }
    }

    private void processSelectedKeysOptimized() {
        // NOTE: 通过数组进行遍历
        for (int i = 0; i < selectedKeys.size; ++i) {
            final SelectionKey k = selectedKeys.keys[i];
            selectedKeys.keys[i] = null;

            // NOTE: attachment 就是 NioChannel
            final Object a = k.attachment();

            if (a instanceof AbstractNioChannel) {
                processSelectedKey(k, (AbstractNioChannel) a);
            }
            else {
                NioTask<SelectableChannel> task = (NioTask<SelectableChannel>) a;
                processSelectedKey(k, task);
            }
        }
    }

    private void processSelectedKeysPlain(Set<SelectionKey> selectedKeys) {
        if (selectedKeys.isEmpty()) {
            return;
        }

        // NOTE: 通过 Iterator 进行遍历
        Iterator<SelectionKey> i = selectedKeys.iterator();
        for (; ; ) {
            final SelectionKey k = i.next();
            final Object a = k.attachment();
            i.remove();

            if (a instanceof AbstractNioChannel) {
                processSelectedKey(k, (AbstractNioChannel) a);
            }
            else {
                NioTask<SelectableChannel> task = (NioTask<SelectableChannel>) a;
                processSelectedKey(k, task);
            }
        }
    }

    private void processSelectedKey(SelectionKey k, AbstractNioChannel ch) {
        final AbstractNioChannel.NioUnsafe unsafe = ch.unsafe();

        int readyOps = k.readyOps();
        if ((readyOps & SelectionKey.OP_CONNECT) != 0) {
            unsafe.finishConnect();
        }

        if ((readyOps & SelectionKey.OP_WRITE) != 0) {
            unsafe.forceFlush();
        }

        if ((readyOps & (SelectionKey.OP_READ | SelectionKey.OP_ACCEPT)) != 0 || readyOps == 0) {
            unsafe.read();
        }
    }
}
```

### 普通任务 + 定时任务

- runAllTasks();
- runAllTasks(long timeoutNanos)

{:refdef: style="text-align: center;"}
![](/assets/images/netty/eventloop/thread/netty-eventloop-task-queue.svg)
{:refdef}

#### 无时间限制

```java
public abstract class SingleThreadEventExecutor extends AbstractScheduledEventExecutor implements OrderedEventExecutor {
    protected boolean runAllTasks() {
        boolean fetchedAll;
        boolean ranAtLeastOne = false;

        do {
            // 第 1 步，将 任务 从 scheduledTaskQueue 转移到 taskQueue
            fetchedAll = fetchFromScheduledTaskQueue();
            // 第 2 步，执行 taskQueue 中的任务
            if (runAllTasksFrom(taskQueue)) {
                ranAtLeastOne = true;
            }
        } while (!fetchedAll); // keep on processing until we fetched all scheduled tasks.

        if (ranAtLeastOne) {
            lastExecutionTime = getCurrentTimeNanos();
        }

        // 第 3 步，执行 tailTasks 中的任务
        afterRunningAllTasks();
        return ranAtLeastOne;
    }
}
```

#### 有时间限制

```java
public abstract class SingleThreadEventExecutor extends AbstractScheduledEventExecutor implements OrderedEventExecutor {
    protected boolean runAllTasks(long timeoutNanos) {
        // 第 1 步，将 任务 从 scheduledTaskQueue 转移到 taskQueue
        fetchFromScheduledTaskQueue();
        Runnable task = pollTask();
        if (task == null) {
            // 第 3 步，执行 tailTasks 中的任务
            afterRunningAllTasks();
            return false;
        }

        final long deadline = timeoutNanos > 0 ? getCurrentTimeNanos() + timeoutNanos : 0;
        long runTasks = 0;
        long lastExecutionTime;
        for (; ; ) {
            // 第 2 步，执行 taskQueue 中的任务
            safeExecute(task);

            runTasks++;

            // Check timeout every 64 tasks because nanoTime() is relatively expensive.
            // XXX: Hard-coded value - will make it configurable if it is really a problem.
            if ((runTasks & 0x3F) == 0) {
                lastExecutionTime = getCurrentTimeNanos();
                // 判断时间是否超时
                if (lastExecutionTime >= deadline) {
                    break;
                }
            }

            task = pollTask();
            if (task == null) {
                lastExecutionTime = getCurrentTimeNanos();
                break;
            }
        }

        // 第 3 步，执行 tailTasks 中的任务
        afterRunningAllTasks();
        this.lastExecutionTime = lastExecutionTime;
        return true;
    }
}
```

## IORatio

```java
public final class NioEventLoop extends SingleThreadEventLoop {
    protected void run() {
        for (; ; ) {
            final int ioRatio = this.ioRatio;
            boolean ranTasks;
            if (ioRatio == 100) {
                try {
                    if (strategy > 0) {
                        // NOTE: 执行 Channel IO
                        processSelectedKeys();
                    }
                }
                finally {
                    // NOTE: 处理普通任务
                    // Ensure we always run tasks.
                    ranTasks = runAllTasks();
                }
            }
            else if (strategy > 0) {
                final long ioStartTime = System.nanoTime();
                try {
                    // NOTE: 执行 Channel IO
                    processSelectedKeys();
                }
                finally {
                    // NOTE: 处理普通任务
                    // Ensure we always run tasks.
                    final long ioTime = System.nanoTime() - ioStartTime;
                    ranTasks = runAllTasks(ioTime * (100 - ioRatio) / ioRatio);
                }
            }
            else {
                // NOTE: 处理普通任务
                ranTasks = runAllTasks(0); // This will run the minimum number of tasks
            }
        }
    }
}
```
