---
title: "Unsafe: CompareAndSwap"
sequence: "106"
---

```java
public class HelloWorld {
    private volatile long counter = 0;

    public long getCounter() {
        return counter;
    }
}
```

```java
import sun.misc.Unsafe;

import java.lang.reflect.Field;

public class Program {
    public static void main(String[] args) throws NoSuchFieldException {
        HelloWorld instance = new HelloWorld();
        printValue(instance);

        long counter = instance.getCounter();
        long before = counter;

        Class<?> clazz = HelloWorld.class;
        Field field = clazz.getDeclaredField("counter");

        Unsafe unsafe = UnsafeUtils.getInstance();
        long fieldOffset = unsafe.objectFieldOffset(field);

        while (!unsafe.compareAndSwapLong(instance, fieldOffset, before, before + 1)) {
            before = counter;
        }

        printValue(instance);
    }

    private static void printValue(HelloWorld instance) {
        long counter = instance.getCounter();
        System.out.println(counter);
    }
}
```
