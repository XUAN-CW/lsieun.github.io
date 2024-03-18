---
title: "Method Delegation: @This"
sequence: "113"
---

A typical reason for using the `@This` annotation to gain access to an instance's fields.

- @This 表示被拦截的目标对象，只有拦截实例方法时可用
- @Origin Method，表示被拦截的目标方法，只有拦截方法或静态方法时可用
- @AllArgument Object[] 目标方法的参数
- @Super 表示被拦截的对象只有拦截实例方法时可用
- @SuperClass ，用于调用目标方法
- 把这些信息打印一下

只能在非静态方法里获取到 this

## 示例

### 预期目标

```text
import java.util.Date;

public class Parent {
    public String test(String name, int age, Date date) {
        return String.format("Hello, %s, %d years old. Now is %s", name, age, date);
    }
}
```

```java
import java.io.Serializable;
import java.util.Base64;
import java.util.Date;

public class HelloWorld extends Parent implements Serializable {
    @Override
    public String test(String name, int age, Date date) {
        String str = String.format("%s:%s:%s", name, age, date);
        byte[] bytes = str.getBytes();
        return Base64.getEncoder().encodeToString(bytes);
    }
}
```

```java
import java.util.Date;

public class HelloWorldRun {
    public static void main(String[] args) {
        HelloWorld instance = new HelloWorld();
        String message = instance.test("Tom", 10, new Date());
        System.out.println(message);
    }
}
```

### 编码实现

```java
import net.bytebuddy.implementation.bind.annotation.RuntimeType;
import net.bytebuddy.implementation.bind.annotation.This;

public class HardWorker {
    @RuntimeType
    public static String doWork(@This HelloWorld instance) {
        System.out.println("instance = " + instance);
        return "This is doWork Method";
    }
}
```

```java
import net.bytebuddy.ByteBuddy;
import net.bytebuddy.dynamic.DynamicType;
import net.bytebuddy.implementation.MethodDelegation;
import net.bytebuddy.matcher.ElementMatchers;

public class HelloWorldRebase {
    public static void main(String[] args) throws Exception {
        // 第一步，准备参数
        String className = "sample.HelloWorld";
        Class<?> clazz = Class.forName(className);


        // 第二步，生成类
        ByteBuddy byteBuddy = new ByteBuddy();
        DynamicType.Builder<?> builder = byteBuddy.rebase(clazz);

        builder = builder.method(
                ElementMatchers.named("test")
        ).intercept(
                MethodDelegation.to(HardWorker.class)
        );


        // 第三步，输出结果
        DynamicType.Unloaded<?> unloadedType = builder.make();
        OutputUtils.save(unloadedType);
    }
}
```

内部实现：

```text
public class HelloWorld extends Parent implements Serializable {
    public String test(String var1, int var2, Date var3) {
        return HardWorker.doWork(this);
    }
}
```

## @This 的参数类型

If the annotated parameter is not assignable to an instance of the dynamic type,
the current method is not considered as a candidate for being bound to the source method.

```text
  Object
    |
  Parent
    |
HelloWorld
```

### Class Hierarchy 类型

第 1 种，使用 `Object` 类型，没有问题：

```java
public class HardWorker {
    @RuntimeType
    public static String doWork(@This Object instance) {
        System.out.println("instance = " + instance);
        return "This is doWork Method";
    }
}
```

第 2 种，使用 `Parent` 类型，没有问题：

```java
public class HardWorker {
    @RuntimeType
    public static String doWork(@This Parent instance) {
        System.out.println("instance = " + instance);
        return "This is doWork Method";
    }
}
```

第 3 种，使用 `Serializable` 类型，没有问题：

```java
public class HardWorker {
    @RuntimeType
    public static String doWork(@This Serializable instance) {
        System.out.println("instance = " + instance);
        return "This is doWork Method";
    }
}
```

### Non-Class-Hierarchy 类型

第 4 种，使用 `Date` 类型，会出错：

```java
public class HardWorker {
    @RuntimeType
    public static String doWork(@This Date instance) {
        System.out.println("instance = " + instance);
        return "This is doWork Method";
    }
}
```
