---
title: "wait and notify"
sequence: "101"
---


## wait/notify 原理

{:refdef: style="text-align: center;"}
![](/assets/images/java/concurrency/obj/obj-monitor-state-waiting-and-blocked.png)
{:refdef}

- Runnable --> Waiting: Owner 线程发现条件不满足，调用 `wait` 方法，即可进入 WaitSet 变为 `WAITING` 状态
- `BLOCKED` 和 `WAITING` 的线程都处于阻塞状态，不占用 CPU 时间片
- Blocked --> Runnable: `BLOCKED` 线程会在 Owner 线程释放锁时唤醒
- Waiting --> Runnable: `WAITING` 线程会在 Owner 线程调用 `notify` 或 `notifyAll` 时唤醒，但唤醒后并不意味者立刻获得锁，仍需进入 EntryList 重新竞争


## API 介绍

- `obj.wait()` 让进入 object 监视器的线程到 waitSet 等待
- `obj.notify()` 在 object 上正在 waitSet 等待的线程中挑一个唤醒
- `obj.notifyAll()` 让 object 上正在 waitSet 等待的所有线程全部唤醒

{:refdef: style="text-align: center;"}
![](/assets/images/java/concurrency/obj/obj-monitor-owner-entry-set-wait-set-trim.gif)
{:refdef}

它们都是线程之间进行协作的手段，都属于 Object 对象的方法。

必须获得此对象的锁，才能调用这几个方法

```java
public class ObjectWaitNotify_001_Wait_A_Without_Sync {
    // 使用 final 修饰，避免 obj 指向别的对象实例
    private static final Object obj = new Object();

    public static void main(String[] args) {
        try {
            obj.wait(3000); // IllegalMonitorStateException: current thread is not owner
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        }
    }
}
```

出现错误：

```text
Exception in thread "main" java.lang.IllegalMonitorStateException: current thread is not owner
```

正确写法：

```java
public class ObjectWaitNotify_001_Wait_B_With_Sync {
    // 使用 final 修饰，避免 obj 指向别的对象实例
    private static final Object obj = new Object();

    public static void main(String[] args) {
        // 必须先获取锁对象之后，才能调用 wait 方法
        synchronized (obj) {
            try {
                obj.wait(3000);
            } catch (InterruptedException ex) {
                ex.printStackTrace();
            }
        }
    }
}
```

## notify与notifyAll

```java
public class ObjectWaitNotify_002_Notify {
    // 使用 final 修饰，避免 obj 指向别的对象实例
    private static final Object obj = new Object();

    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            synchronized (obj) {
                LogUtils.log("火遁");
                try {
                    obj.wait();
                } catch (InterruptedException ex) {
                    ex.printStackTrace();
                }
                LogUtils.log("豪火球");
            }
        }, "t1");
        t1.start();

        Thread t2 = new Thread(() -> {
            synchronized (obj) {
                LogUtils.log("水遁");
                try {
                    obj.wait();
                } catch (InterruptedException ex) {
                    ex.printStackTrace();
                }
                LogUtils.log("水龙弹");
            }
        }, "t2");
        t2.start();

        sleep(1);
        LogUtils.log("唤醒 obj-Monitor-WaitSet 的线程");
        synchronized (obj) {
            // obj.notify();    // 唤醒obj上一个线程
            obj.notifyAll(); // 唤醒obj上所有等待线程
        }

        sleep(3);
        System.exit(0);
    }
}
```

## wait 和 notify 的正确使用方式

```text
synchronized(lock) {
    while(条件不成立) {
        lock.wait();
    }
    // 干活
}

//另一个线程
synchronized(lock) {
    lock.notifyAll();
}
```

## sleep 和 wait 的区别

sleep(long n) 和 wait(long n) 的区别

- 相同：两者都是 `TIMED_WAITING` 状态
- 不同
  - `sleep` 是 `Thread` 方法，而 `wait` 是 `Object` 的方法
  - `sleep` 不需要强制和 `synchronized` 配合使用，但 `wait` 需要和 `synchronized` 一起用
  - `sleep` 在睡眠的同时，不会释放对象锁的，但 `wait` 在等待的时候会释放对象锁


## Reference

- [Inside the Java Virtual Machine: Thread Synchronization](https://www.artima.com/insidejvm/ed2/threadsynchP.html) 写的好
- [wait and notify() Methods in Java](https://www.baeldung.com/java-wait-notify)
- [Difference Between Wait and Sleep in Java](https://www.baeldung.com/java-wait-and-sleep)
