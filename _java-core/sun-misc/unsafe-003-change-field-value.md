---
title: "Unsafe: change field value"
sequence: "103"
---

```java
public class HelloWorld {
    private final int intValue;

    public HelloWorld() {
        this.intValue = 10;
    }

    public int getIntValue() {
        return intValue;
    }
}
```

```java
import java.lang.reflect.Field;

public class Program {
    public static void main(String[] args) throws NoSuchFieldException, IllegalAccessException {
        HelloWorld instance = new HelloWorld();
        printValue(instance); // 10

        // 通过反射修改
        Class<?> clazz = HelloWorld.class;
        Field field = clazz.getDeclaredField("intValue");
        field.setAccessible(true);
        field.set(instance, 20);

        printValue(instance); // 20
    }

    private static void printValue(HelloWorld instance) {
        int intValue = instance.getIntValue();
        System.out.println(intValue);
    }
}
```

```java
import sun.misc.Unsafe;

import java.lang.reflect.Field;

public class Program {
    public static void main(String[] args) throws NoSuchFieldException {
        HelloWorld instance = new HelloWorld();
        printValue(instance); // 10

        // 通过 Unsafe 修改
        Class<?> clazz = HelloWorld.class;
        Field field = clazz.getDeclaredField("intValue");
        Unsafe unsafe = UnsafeUtils.getInstance();
        long fieldOffset = unsafe.objectFieldOffset(field);
        unsafe.putInt(instance, fieldOffset, 30);

        printValue(instance); // 30
    }

    private static void printValue(HelloWorld instance) {
        int intValue = instance.getIntValue();
        System.out.println(intValue);
    }
}
```
