---
title: "Unsafe: Off-Heap Memory"
sequence: "105"
---

If an application is running out of available memory on the JVM,
we could end up forcing the GC process to run too often.
Ideally, we would want a special memory region, off-heap and not controlled by the GC process.

The `allocateMemory()` method from the `Unsafe` class gives us the ability to allocate huge objects off the heap,
meaning that this memory will not be seen and taken into account by the **GC** and the **JVM**.

This can be very useful, but we need to remember that
this memory needs to be managed manually and properly reclaiming with `freeMemory()` when no longer needed.

```java
import sun.misc.Unsafe;

public class Program {
    public static void main(String[] args) {
        Unsafe unsafe = UnsafeUtils.getInstance();

        long size = 1024L;
        long address = unsafe.allocateMemory(size);

        for (int i = 0; i < 10; i++) {
            unsafe.putByte(address + i, (byte) ('a' + i));
        }

        for (int i = 0; i < 10; i++) {
            byte b = unsafe.getByte(address + i);
            char ch = (char) b;
            System.out.println(ch);
        }

        unsafe.freeMemory(address);
    }
}
```
