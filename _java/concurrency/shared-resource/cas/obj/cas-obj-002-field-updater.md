---
title: "字段更新器"
sequence: "102"
---

- AtomicReferenceFieldUpdater //  域    字段
- AtomicIntegerFieldUpdater
- AtomicLongFieldUpdater

利用字段更新器，可以针对对象的某个域（Field）进行原子操作，只能配合 `volatile` 修饰的字段使用，
否则会出现异常

```text
Exception in thread "main" java.lang.IllegalArgumentException: Must be volatile type
```

```java
import java.util.concurrent.atomic.AtomicIntegerFieldUpdater;

public class FieldUpdaterRun {
    private volatile int field;

    public static void main(String[] args) {
        AtomicIntegerFieldUpdater<FieldUpdaterRun> fieldUpdater =
                AtomicIntegerFieldUpdater.newUpdater(FieldUpdaterRun.class, "field");

        FieldUpdaterRun instance = new FieldUpdaterRun();
        fieldUpdater.compareAndSet(instance, 0, 10);

        // 修改成功 field = 10
        System.out.println(instance.field);

        // 修改成功 field = 20
        fieldUpdater.compareAndSet(instance, 10, 20);
        System.out.println(instance.field);

        // 修改失败 field = 20
        fieldUpdater.compareAndSet(instance, 10, 30);
        System.out.println(instance.field);
    }
}
```
