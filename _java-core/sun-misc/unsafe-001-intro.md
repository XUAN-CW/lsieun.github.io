---
title: "Unsafe"
sequence: "101"
---

## Unsafe

```java
/**
 * A collection of methods for performing low-level, unsafe operations.
 * Although the class and all methods are public, use of this class is
 * limited because only trusted code can obtain instances of it.
 *
 */

public final class Unsafe {
    /**
     * Report the location of a given field in the storage allocation of its
     * class.  Do not expect to perform any sort of arithmetic on this offset;
     * it is just a cookie which is passed to the unsafe heap memory accessors.
     *
     * <p>Any given field will always have the same offset and base, and no
     * two distinct fields of the same class will ever have the same offset
     * and base.
     *
     * <p>As of 1.4.1, offsets for fields are represented as long values,
     * although the Sun JVM does not use the most significant 32 bits.
     * However, JVM implementations which store static fields at absolute
     * addresses can use long offsets and null base pointers to express
     * the field locations in a form usable by {@link #getInt(Object,long)}.
     * Therefore, code which will be ported to such JVMs on 64-bit platforms
     * must preserve all bits of static field offsets.
     * @see #getInt(Object, long)
     */
    public native long staticFieldOffset(Field f);

    /**
     * Report the location of a given static field, in conjunction with {@link
     * #staticFieldBase}.
     * <p>Do not expect to perform any sort of arithmetic on this offset;
     * it is just a cookie which is passed to the unsafe heap memory accessors.
     *
     * <p>Any given field will always have the same offset, and no two distinct
     * fields of the same class will ever have the same offset.
     *
     * <p>As of 1.4.1, offsets for fields are represented as long values,
     * although the Sun JVM does not use the most significant 32 bits.
     * It is hard to imagine a JVM technology which needs more than
     * a few bits to encode an offset within a non-array object,
     * However, for consistency with other methods in this class,
     * this method reports its result as a long value.
     * @see #getInt(Object, long)
     */
    public native long objectFieldOffset(Field f);
    
    /**
     * Fetches a reference value from a given Java variable, with volatile
     * load semantics. Otherwise identical to {@link #getObject(Object, long)}
     */
    public native Object getObjectVolatile(Object o, long offset);

    /**
     * Stores a reference value into a given Java variable, with
     * volatile store semantics. Otherwise identical to {@link #putObject(Object, long, Object)}
     */
    public native void putObjectVolatile(Object o, long offset, Object x);
    
    /**
     * Tell the VM to define a class, without security checks.
     * By default, the class loader and protection domain come from the caller's class.
     */
    public native Class<?> defineClass(String name, byte[] b, int off, int len,
                                       ClassLoader loader,
                                       ProtectionDomain protectionDomain);

    /**
     * Define a class but do not make it known to the class loader or system dictionary.
     * <p>
     * @param hostClass context for linkage, access control, protection domain, and class loader
     * @param data      bytes of a class file
     * @param cpPatches where non-null entries exist, they replace corresponding CP entries in data
     */
    public native Class<?> defineAnonymousClass(Class<?> hostClass, byte[] data, Object[] cpPatches);
}
```

### compare and swap

```java
public final class Unsafe {
    /**
     * Atomically update Java variable to <tt>x</tt> if it is currently
     * holding <tt>expected</tt>.
     * @return <tt>true</tt> if successful
     */
    public final native boolean compareAndSwapObject(Object o, long offset,
                                                     Object expected,
                                                     Object x);

    /**
     * Atomically update Java variable to <tt>x</tt> if it is currently
     * holding <tt>expected</tt>.
     * @return <tt>true</tt> if successful
     */
    public final native boolean compareAndSwapInt(Object o, long offset,
                                                  int expected,
                                                  int x);

    /**
     * Atomically update Java variable to <tt>x</tt> if it is currently
     * holding <tt>expected</tt>.
     * @return <tt>true</tt> if successful
     */
    public final native boolean compareAndSwapLong(Object o, long offset,
                                                   long expected,
                                                   long x);
}
```

## Create Instance

```java
public final class Unsafe {
    @CallerSensitive
    public static Unsafe getUnsafe() {
        Class<?> caller = Reflection.getCallerClass();
        if (!VM.isSystemDomainLoader(caller.getClassLoader()))
            throw new SecurityException("Unsafe");
        return theUnsafe;
    }
}
```

```java
import sun.misc.Unsafe;

public class HelloWorld {
    public static void main(String[] args) {
        Unsafe unsafe = Unsafe.getUnsafe();
    }
}
```

```text
Exception in thread "main" java.lang.SecurityException: Unsafe
```

```java
import sun.misc.Unsafe;

import java.lang.reflect.Field;

public class HelloWorld {
    public static void main(String[] args) throws IllegalAccessException, NoSuchFieldException {
        Field f = Unsafe.class.getDeclaredField("theUnsafe");
        f.setAccessible(true);
        Unsafe unsafe = (Unsafe) f.get(null);
    }
}
```

