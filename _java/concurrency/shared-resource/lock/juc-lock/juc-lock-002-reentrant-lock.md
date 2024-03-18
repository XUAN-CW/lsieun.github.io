---
title: "ReentrantLock - 重入锁"
sequence: "102"
---

## 基本介绍

重入锁，是指任意线程，在获取锁之后，再次获取该锁而不会被锁阻塞。

### ReentrantLock 类

`ReentrantLock` 类实现了 `Lock` 接口：

```java
public class ReentrantLock implements Lock, Serializable {
    // ...
}
```

It offers the same concurrency and memory semantics
as the **implicit monitor lock** accessed
using `synchronized` methods and statements, with extended capabilities.

### 与 synchronized 对比

相对于 synchronized 它具备如下特点

- 不同点
    - 可中断
    - 可以设置超时时间
    - 可以设置为公平锁
    - 支持多个条件变量
- 相同点
    - 与 synchronized 一样，都支持可重入

### 如何使用

```text
// 获取锁
reentrantLock.lock();
try {
    // 临界区
} finally {
    // 释放锁
    reentrantLock.unlock();        
}
```

```text
// 第 1 步，创建对象
ReentrantLock lock = new ReentrantLock();

try {
    // 第 2 步，调用 lock 方法
    lock.lock();
    // do something
}
finally {
    // 第 3 步，调用 unlock 方法
    // 要考虑发生异常的情况，放在 finally 里，确定 unlock 方法一定会调用
    lock.unlock();
}
```

## 特性

### 可重入

经典方式：

```java
import java.util.concurrent.locks.ReentrantLock;

public class LockReentrantRun {
    private static final ReentrantLock lock = new ReentrantLock();

    public static void main(String[] args) {
        method1();
    }

    public static void method1() {
        lock.lock();
        try {
            LogUtils.log("execute method1");
            method2();
        } finally {
            lock.unlock();
        }
    }

    public static void method2() {
        lock.lock();
        try {
            LogUtils.log("execute method2");
            method3();
        } finally {
            lock.unlock();
        }
    }

    public static void method3() {
        lock.lock();
        try {
            LogUtils.log("execute method3");
        } finally {
            lock.unlock();
        }
    }

}
```

输出：

```text
43:35.512 [main] INFO execute method1
43:35.513 [main] INFO execute method2
43:35.513 [main] INFO execute method3
```

一个递归的方式：

```java
import java.util.concurrent.locks.ReentrantLock;

public class LockReentrantRun {
    private static final ReentrantLock lock = new ReentrantLock();

    public static void main(String[] args) {
        work(1, 3);
    }

    private static void work(int currentDepth, int maxDepth) {
        if (currentDepth > maxDepth) {
            return;
        }

        try {
            LogUtils.log("lock: i = {}", currentDepth);
            lock.lock();
            work(currentDepth + 1, maxDepth);
        } finally {
            lock.unlock();
            LogUtils.log("unlock: i = {}", currentDepth);
        }
    }
}
```

输出：

```text
39:12.690 [main] INFO lock: i = 1
39:12.692 [main] INFO lock: i = 2
39:12.692 [main] INFO lock: i = 3
39:12.692 [main] INFO unlock: i = 3
39:12.692 [main] INFO unlock: i = 2
39:12.692 [main] INFO unlock: i = 1
```

### 可打断

```java
import java.util.concurrent.locks.ReentrantLock;

import static lsieun.concurrent.utils.SleepUtils.sleep;

public class LockInterruptRun {
    public static void main(String[] args) {
        ReentrantLock lock = new ReentrantLock();

        Thread t1 = new Thread(() -> {
            LogUtils.log("启动...");
            try {
                lock.lockInterruptibly();
            } catch (InterruptedException e) {
                e.printStackTrace();
                LogUtils.log("等锁的过程中被打断");
                return;
            }
            try {
                LogUtils.log("获得了锁");
            } finally {
                lock.unlock();
            }
        }, "t1");

        lock.lock();
        LogUtils.log("获得了锁");
        t1.start();
        try {
            sleep(1);
            t1.interrupt();
            LogUtils.log("执行打断");
        } finally {
            lock.unlock();
        }
    }

}
```

### 超时

```text
lock.tryLock()
lock.tryLock(1, TimeUnit.SECONDS)
```

```text
public void performTryLock(){
    boolean isLockAcquired = lock.tryLock(1, TimeUnit.SECONDS);
    
    if(isLockAcquired) {
        try {
            // Critical section here
        } finally {
            lock.unlock();
        }
    }
}
```

立刻失败

```java
import java.util.concurrent.locks.ReentrantLock;

import static lsieun.concurrent.utils.SleepUtils.sleep;

public class LockTimeoutRun {
    public static void main(String[] args) {
        ReentrantLock lock = new ReentrantLock();

        Thread t1 = new Thread(() -> {
            LogUtils.log("启动...");
            if (!lock.tryLock()) {
                LogUtils.log("获取立刻失败，返回");
                return;
            }
            try {
                LogUtils.log("获得了锁");
            } finally {
                lock.unlock();
            }
        }, "t1");

        lock.lock();
        LogUtils.log("获得了锁");
        t1.start();
        try {
            sleep(2);
        } finally {
            lock.unlock();
        }
    }

}
```

超时失败

```java
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.ReentrantLock;


public class LockTimeoutRun {
    public static void main(String[] args) {
        ReentrantLock lock = new ReentrantLock();
        Thread t1 = new Thread(() -> {
            LogUtils.log("启动...");
            try {
                if (!lock.tryLock(2, TimeUnit.SECONDS)) {
                    LogUtils.log("获取等待 2s 后失败，返回");
                    return;
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            try {
                LogUtils.log("获取等待 1s 后成功，获得了锁");
            } finally {
                lock.unlock();
            }
        }, "t1");

        lock.lock();
        LogUtils.log("获得了锁");
        t1.start();
        try {
            sleep(1);
        } finally {
            lock.unlock();
        }
    }

}
```

### 公平锁

`ReentrantLock` 默认是不公平的。

```text
Lock nonFairLock1 = new ReentrantLock();         // A non-fair lock (Default is non-fair)
Lock nonFairLock2 = new ReentrantLock(false);    // A non-fair lock
Lock fairLock = new ReentrantLock(true);         // A fair lock
```

- 公平锁：保证“先来，先获取锁；后来，后获取锁”的顺序
    - 缺点：公平锁一般没有必要，会降低并发度。
- 非公平锁：不能保证顺序
    - 缺点：在一些特殊情况下，有的线程总是拿不到锁

```java
import java.util.concurrent.locks.ReentrantLock;


public class LockFairRun {
    public static void main(String[] args) {
        ReentrantLock lock = new ReentrantLock(false);
        lock.lock();
        for (int i = 0; i < 500; i++) {
            new Thread(() -> {
                lock.lock();
                try {
                    LogUtils.log("running");
                } finally {
                    lock.unlock();
                }
            }, "t" + i).start();
        }

        // 1s 之后去争抢锁
        sleep(1);
        new Thread(() -> {
            LogUtils.log("start...");
            lock.lock();
            try {
                LogUtils.log("running");
            } finally {
                lock.unlock();
            }
        }, "强行插入").start();
        lock.unlock();
    }
}
```

强行插入，有机会在中间输出

注意：该实验不一定总能复现

### 条件变量

synchronized 中也有条件变量，就是我们讲原理时那个 waitSet 休息室，当条件不满足时进入 waitSet 等待

ReentrantLock 的条件变量比 synchronized 强大之处在于，它是支持多个条件变量的，这就好比

- synchronized 是那些不满足条件的线程都在一间休息室等消息
- 而 ReentrantLock 支持多间休息室，有专门等烟的休息室、专门等早餐的休息室、唤醒时也是按休息室来唤醒

使用要点：

- await 前需要获得锁
- await 执行后，会释放锁，进入 conditionObject 等待
- await 的线程被唤醒（或打断、或超时）取重新竞争 lock 锁
- 竞争 lock 锁成功后，从 await 后继续执行

```java
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

import static lsieun.concurrent.utils.SleepUtils.sleep;

public class LockConditionRun {
    static boolean hasCigarette = false;
    static boolean hasTakeout = false;
    static ReentrantLock ROOM = new ReentrantLock();
    // 等待烟的休息室
    static Condition waitCigaretteSet = ROOM.newCondition();
    // 等外卖的休息室
    static Condition waitTakeoutSet = ROOM.newCondition();

    public static void main(String[] args) {


        new Thread(() -> {
            ROOM.lock();
            try {
                LogUtils.log("有烟没？[{}]", hasCigarette);
                while (!hasCigarette) {
                    LogUtils.log("没烟，先歇会！");
                    try {
                        waitCigaretteSet.await();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                LogUtils.log("可以开始干活了");
            } finally {
                ROOM.unlock();
            }
        }, "小南").start();

        new Thread(() -> {
            ROOM.lock();
            try {
                LogUtils.log("外卖送到没？[{}]", hasTakeout);
                while (!hasTakeout) {
                    LogUtils.log("没外卖，先歇会！");
                    try {
                        waitTakeoutSet.await();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                LogUtils.log("可以开始干活了");
            } finally {
                ROOM.unlock();
            }
        }, "小女").start();

        sleep(1);
        new Thread(() -> {
            ROOM.lock();
            try {
                hasTakeout = true;
                waitTakeoutSet.signal();
            } finally {
                ROOM.unlock();
            }
        }, "送外卖的").start();

        sleep(1);

        new Thread(() -> {
            ROOM.lock();
            try {
                hasCigarette = true;
                waitCigaretteSet.signal();
            } finally {
                ROOM.unlock();
            }
        }, "送烟的").start();
    }

}
```

## 示例代码

### 求和

```text
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.locks.ReentrantLock;

public class Sum {
    public static void main(String[] args) {
        SharedObjectWithLock instance = new SharedObjectWithLock();

        List<Thread> threadList = new ArrayList<>();
        for (int i = 0; i < 100; i++) {
            Thread t = new Thread(() -> {
                for (int j = 0; j < 10000; j++) {
                    instance.perform();
                }
            });
            threadList.add(t);
        }

        threadList.forEach(Thread::start);
        threadList.forEach(t -> {
            try {
                t.join();
            } catch (InterruptedException ex) {
                ex.printStackTrace();
            }
        });

        int counter = instance.getCounter();
        LogUtils.log("counter = {}", counter);
    }
}


class SharedObjectWithLock {
    final ReentrantLock lock = new ReentrantLock();
    int counter = 0;

    public void perform() {
        lock.lock();
        try {
            // Critical section here
            counter++;
        } finally {
            lock.unlock();
        }
    }

    public int getCounter() {
        return counter;
    }
}
```

### Lock 接口

```java
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class ThreadExample implements Runnable {

    final Lock lock;

    public ThreadExample(final Lock lock) {
        this.lock = lock;
    }

    @Override
    public void run() {
        while (true) {
            try {
                if (lock.tryLock(1, TimeUnit.SECONDS)) {
                    try {
                        LogUtils.log("acquire lock");
                        TimeUnit.SECONDS.sleep(2);
                    } finally {
                        lock.unlock();
                        LogUtils.log("release lock");
                    }
                    break;
                } else {
                    LogUtils.log("unable to acquire the lock");
                }
            } catch (InterruptedException ignore) {
            }
        }
    }

    public static void main(String[] args) {
        final Lock lock = new ReentrantLock();
        new Thread(new ThreadExample(lock), "thread_1").start();
        new Thread(new ThreadExample(lock), "thread_2").start();
    }
}
```

```text
13:49.605 [thread_1] INFO acquire lock
13:50.517 [thread_2] INFO unable to acquire the lock
13:51.528 [thread_2] INFO unable to acquire the lock
13:51.608 [thread_1] INFO release lock
13:51.608 [thread_2] INFO acquire lock
13:53.616 [thread_2] INFO release lock
```

### 哲学家就餐问题

```java
import java.util.concurrent.locks.ReentrantLock;

public class PhilosopherRun {
    public static void main(String[] args) {
        Chopstick c1 = new Chopstick("1");
        Chopstick c2 = new Chopstick("2");
        Chopstick c3 = new Chopstick("3");
        Chopstick c4 = new Chopstick("4");
        Chopstick c5 = new Chopstick("5");
        new Philosopher("苏格拉底", c1, c2).start();
        new Philosopher("柏拉图", c2, c3).start();
        new Philosopher("亚里士多德", c3, c4).start();
        new Philosopher("赫拉克利特", c4, c5).start();
        new Philosopher("阿基米德", c5, c1).start();
    }
}

class Philosopher extends Thread {
    Chopstick left;
    Chopstick right;

    public Philosopher(String name, Chopstick left, Chopstick right) {
        super(name);
        this.left = left;
        this.right = right;
    }

    @Override
    public void run() {
        while (true) {
            //　尝试获得左手筷子
            if (left.tryLock()) {
                try {
                    // 尝试获得右手筷子
                    if (right.tryLock()) {
                        try {
                            eat();
                        } finally {
                            right.unlock();
                        }
                    }
                } finally {
                    // 获取右手筷子失败，会放弃已经拿到的左手筷子
                    left.unlock();
                }
            }
        }
    }

    private void eat() {
        LogUtils.log("eating...");
        SleepUtils.sleep(1);
    }
}


class Chopstick extends ReentrantLock {
    String name;

    public Chopstick(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "筷子{" + name + '}';
    }
}
```

只吃一次：

```java
import java.util.concurrent.locks.ReentrantLock;

public class PhilosopherRun {
    public static void main(String[] args) {
        Chopstick c1 = new Chopstick("1");
        Chopstick c2 = new Chopstick("2");
        Chopstick c3 = new Chopstick("3");
        Chopstick c4 = new Chopstick("4");
        Chopstick c5 = new Chopstick("5");
        new Philosopher("苏格拉底", c1, c2).start();
        new Philosopher("柏拉图", c2, c3).start();
        new Philosopher("亚里士多德", c3, c4).start();
        new Philosopher("赫拉克利特", c4, c5).start();
        new Philosopher("阿基米德", c5, c1).start();
    }
}

class Philosopher extends Thread {
    Chopstick left;
    Chopstick right;

    public Philosopher(String name, Chopstick left, Chopstick right) {
        super(name);
        this.left = left;
        this.right = right;
    }

    @Override
    public void run() {
        while (true) {
            boolean success = false;
            //　尝试获得左手筷子
            if (left.tryLock()) {
                try {
                    // 尝试获得右手筷子
                    if (right.tryLock()) {
                        try {
                            eat();
                            success = true;
                        } finally {
                            right.unlock();
                        }
                    }
                } finally {
                    // 获取右手筷子失败，会放弃已经拿到的左手筷子
                    left.unlock();
                }
            }

            if (success) {
                break;
            }
        }
    }

    private void eat() {
        LogUtils.log("eating...");
        SleepUtils.sleep(1);
    }
}


class Chopstick extends ReentrantLock {
    String name;

    public Chopstick(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "筷子{" + name + '}';
    }
}
```

吃指定次数（例如，三次）：

```java
import java.util.concurrent.locks.ReentrantLock;

public class PhilosopherRun {
    public static void main(String[] args) {
        Chopstick c1 = new Chopstick("1");
        Chopstick c2 = new Chopstick("2");
        Chopstick c3 = new Chopstick("3");
        Chopstick c4 = new Chopstick("4");
        Chopstick c5 = new Chopstick("5");
        new Philosopher("苏格拉底", c1, c2).start();
        new Philosopher("柏拉图", c2, c3).start();
        new Philosopher("亚里士多德", c3, c4).start();
        new Philosopher("赫拉克利特", c4, c5).start();
        new Philosopher("阿基米德", c5, c1).start();
    }
}

class Philosopher extends Thread {
    Chopstick left;
    Chopstick right;

    public Philosopher(String name, Chopstick left, Chopstick right) {
        super(name);
        this.left = left;
        this.right = right;
    }

    @Override
    public void run() {
        int count = 0;
        while (true) {
            //　尝试获得左手筷子
            if (left.tryLock()) {
                try {
                    // 尝试获得右手筷子
                    if (right.tryLock()) {
                        try {
                            eat();
                            count++;
                        } finally {
                            right.unlock();
                        }
                    }
                } finally {
                    // 获取右手筷子失败，会放弃已经拿到的左手筷子
                    left.unlock();
                }
            }

            if (count == 3) {
                break;
            }
        }
    }

    private void eat() {
        LogUtils.log("eating...");
        SleepUtils.sleep(1);
    }
}


class Chopstick extends ReentrantLock {
    String name;

    public Chopstick(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "筷子{" + name + '}';
    }
}
```

