---
title: "内存屏障"
sequence: "102"
---

```text
The Java Language Specification (JLS) doesn't refer to barriers explicitly,
as it considers them to be implementation details
that operate based on the concept of happens before semantics.
Implementing proper specifications for these semantics in accordance with the JMM ( Java Memory Model)
would require significant changes to the JMM.
```

## What's a Memory Barrier?

It's a CPU instruction.

Basically it's an instruction to

- a) ensure the **order** in which certain operations are executed and
- b) influence **visibility** of some data (which might be the result of executing some instruction).

Compilers and CPUs can re-order instructions, provided the end result is the same, to try and optimise performance.
**Inserting a memory barrier** tells the **CPU** and the **compiler** that
**what happened before that command needs to stay before that command,
and what happens after needs to stay after.**

{:refdef: style="text-align: center;"}
![](/assets/images/java/concurrency/memory/memory-barrier.png)
{:refdef}

The other thing a memory barrier does is **force an update of the various CPU caches** - for example,
a write barrier will flush all the data that was written before the barrier out to cache,
therefore any other thread that tries to read that data will get the most up-to-date version
regardless of which core or which socket it might be executing by.

## What's this got to do with Java?

The magic incantation here is the word `volatile`.
If your field is `volatile`, the Java Memory Model inserts
a write barrier instruction after you write to it,
and a read barrier instruction before you read from it.

{:refdef: style="text-align: center;"}
![](/assets/images/java/concurrency/memory/memory-barrier-write.png)
{:refdef}

This means if you write to a `volatile` field, you know that:

- Any thread accessing that field after the point at which you wrote to it will get the updated value
- Anything you did before you wrote that field is guaranteed to have happened and any updated data values will also be visible, because the memory barrier flushed all earlier writes to the cache.

## 不同的实现

Memory barriers are a complex subject.
They are implemented very differently across CPU architectures.

## Barrier

### Store Barrier

A store barrier, "sfence" instruction on x86,
forces all store instructions prior to the barrier to happen before the barrier and
have the store buffers flushed to cache for the CPU on which it is issued.
This will make the program state visible to other CPUs, so they can act on it if necessary.

### Load Barrier

A load barrier, "lfence" instruction on x86,
forces all load instructions after the barrier to happen after the barrier and
then wait on the load buffer to drain for that CPU.
This makes program state exposed from other CPUs visible to this CPU before making further progress.


### Full Barrier

A full barrier, "mfence" instruction on x86,
is a composite of both load and store barriers happening on a CPU.

## 添加位置

### volatile

In the Java Memory Model,
a `volatile` field has a **store barrier** inserted after a write to it and
a **load barrier** inserted before a read of it.

### final

Qualified `final` fields of a class have a **store barrier** inserted after their initialisation
to ensure these fields are visible once the constructor completes
when a reference to the object is available.

## Atomic Instructions and Software Locks

Atomic instructions, such as the “lock ...” instructions on x86,
are effectively **a full barrier** as they lock the memory sub-system
to perform an operation and have guaranteed total order, even across CPUs.

Software locks usually employ memory barriers, or atomic instructions,
to achieve visibility and preserve program order.

## Performance Impact of Memory Barriers

Memory barriers, being another CPU-level instruction,
don't have the same cost as locks - the kernel isn't interfering and arbitrating between multiple threads.
But nothing comes for free.
Memory barriers do have a cost - the compiler/CPU cannot re-order instructions,
which could potentially lead to not using the CPU as efficiently as possible,
and refreshing the caches obviously has a performance impact.
So don't think that using `volatile` instead of locking will get you away scot-free.

```text
memory barrier 也对性能有影响
```

Memory barriers are CPU instructions that allow you to make certain assumptions about
when data will be visible to other processes.
In Java, you implement them with the `volatile` keyword.
Using `volatile` means you don't necessarily have to add locks willy-nilly,
and will give you performance improvements over using them.
However, you need to think a little more carefully about your design,
in particular how frequently you use `volatile` fields, and how frequently you read and write them.

```text
使用 volatile 比使用 lock 的效率要高一些，但是还是需要注意
```

Memory barriers prevent a CPU from performing a lot of techniques to hide memory latency
therefore they have **a significant performance cost** which must be considered.

To achieve maximum performance, it is best to model the problem
so the processor can do units of work,
then have all the necessary memory barriers occur on the boundaries of these work units.

Taking this approach allows the processor to optimise the units of work without restriction.
There is an advantage to grouping necessary memory barriers in that
buffers flushed after the first one will be less costly
because no work will be under way to refill them.

## Reference

- [x] [Dissecting the Disruptor: Demystifying Memory Barriers](https://trishagee.com/2011/08/07/dissecting_the_disruptor_demystifying_memory_barriers/)
- [x] [Memory Barriers/Fences](https://mechanical-sympathy.blogspot.com/2011/07/memory-barriersfences.html)
- [Memory Barriers and JVM Concurrency](https://www.infoq.com/articles/memory_barriers_jvm_concurrency/)
- [Deep Dive Into Java Memory Model](https://eksimtech.com/deep-dive-into-java-memory-model-29f7ed4d6ceb)
- [ ] [JSR 133 (Java Memory Model) FAQ](https://www.cs.umd.edu/~pugh/java/memoryModel/jsr-133-faq.html)
- [ ] [The JSR-133 Cookbook for Compiler Writers](https://gee.cs.oswego.edu/dl/jmm/cookbook.html)


- [Java Memory Fences: Their Purpose and Function](https://copyprogramming.com/howto/what-are-memory-fences-used-for-in-java)
