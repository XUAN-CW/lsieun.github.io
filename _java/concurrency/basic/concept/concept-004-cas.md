---
title: "CAS"
sequence: "104"
---

Compare and Swap

## CAS 原理

CAS 全称是 compare and swap(比较并且交换)，是一种用于在多线程环境下实现同步功能的机制，其也是无锁优化，或者叫自旋，还有自适应自旋。

在 JDK 中，CAS 加 `volatile` 关键字作为实现并发包的基石。
没有 CAS 就不会有并发包，`java.util.concurrent` 中借助了 CAS 指令实现了一种区别于 `synchronized` 的一种乐观锁。



## CAS 的缺陷

### ABA 问题

### 循环时间长开销大

自旋 CAS（不成功，就一直循环执行，直到成功）如果长时间不成功，会给 CPU 带来极大的执行开销。

解决方法：

- 限制自旋次数，防止进入死循环
- JVM 能支持处理器提供的 pause 指令那么效率会有一定的提升

### 只能保证一个共享变量的原子操作

当对一个共享变量执行操作时，我们可以使用循环 CAS 的方式来保证原子操作，但是对多个共享变量操作时，循环 CAS 就无法保证操作的原子性

解决方法：

- 如果需要对多个共享变量进行操作，可以使用加锁方式(悲观锁)保证原子性，
- 可以把多个共享变量合并成一个共享变量进行 CAS 操作。

