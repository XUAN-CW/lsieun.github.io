---
title: "Unsafe: allocation instance"
sequence: "102"
---

```java
public class HelloWorld {
    private final int intValue;

    public HelloWorld(int intValue) {
        this.intValue = intValue;
    }

    public int getIntValue() {
        return intValue;
    }
}
```

```java
public class Program {
    public static void main(String[] args) {
        HelloWorld instance = new HelloWorld();
        int intValue = instance.getIntValue();
        System.out.println(intValue); // 10
    }
}
```

```java
import lsieun.utils.UnsafeUtils;
import sun.misc.Unsafe;

public class Program {
    public static void main(String[] args) throws InstantiationException {
        Unsafe unsafe = UnsafeUtils.getInstance();
        HelloWorld instance = (HelloWorld) unsafe.allocateInstance(HelloWorld.class);
        int intValue = instance.getIntValue();
        System.out.println(intValue); // 0
    }
}
```

