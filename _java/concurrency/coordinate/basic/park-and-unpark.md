---
title: "park & unpark"
sequence: "101"
---

## 基本使用

它们是 `LockSupport` 类中的方法

```text
// 暂停当前线程
LockSupport.park();

// 恢复某个线程的运行
LockSupport.unpark(暂停线程对象)
```

先 park 再 unpark

```java
import java.util.concurrent.locks.LockSupport;

public class LockPark {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            LogUtils.log("start...");
            sleep(1);
            LogUtils.log("park...");
            LockSupport.park();
            LogUtils.log("resume...");
        },"t1");
        t1.start();

        sleep(2);
        LogUtils.log("unpark...");
        LockSupport.unpark(t1);
    }
}
```

先 unpark 再 park

```java
import java.util.concurrent.locks.LockSupport;

public class LockPark {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            LogUtils.log("start...");
            sleep(2);
            LogUtils.log("park...");
            LockSupport.park();
            LogUtils.log("resume...");
        },"t1");
        t1.start();

        sleep(1);
        LogUtils.log("unpark...");
        LockSupport.unpark(t1);
    }
}
```

```text
40:56.709 [t1] INFO start...
40:57.632 [main] INFO unpark...
40:58.711 [t1] INFO park...
40:58.711 [t1] INFO resume...
```

## 特点

与 Object 的 wait & notify 相比

- wait，notify 和 notifyAll 必须配合 Object Monitor 一起使用，而 park，unpark 不必
- park & unpark 是以**线程**为单位来【阻塞】和【唤醒】线程，而 notify 只能随机唤醒一个等待线程，notifyAll 是唤醒所有等待线程，就不那么【精确】
- park & unpark 可以先 unpark，而 wait & notify 不能先 notify

