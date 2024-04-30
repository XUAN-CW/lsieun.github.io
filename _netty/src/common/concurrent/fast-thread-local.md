---
title: "FastThreadLocal"
sequence: "101"
---

[UP](/netty.html)

```java
import org.junit.jupiter.api.Test;

public class FastThreadLocalTest {
    public static final FastThreadLocal<String> f1 = new FastThreadLocal<>();
    public static final FastThreadLocal<String> f2 = new FastThreadLocal<>();

    @Test
    void test() {
        FastThreadLocalThread t1 = new FastThreadLocalThread(() -> {
            f1.set("hello");
            f2.set("world");

            Thread thread = Thread.currentThread();
            System.out.println(thread.getId());
        });
        t1.start();
    }
}
```

| Netty                  | JDK            |
|------------------------|----------------|
| InternalThreadLocalMap | ThreadLocalMap |
| FastThreadLocal        | ThreadLocal    |
| FastThreadLocalThread  | Thread         |
