---
title: "Method Delegation: @Argument, @AllArguments"
sequence: "114"
---

索引从 `0` 开始，`0` 表示第一个参数，`1` 表示第二个参数。

```java
import java.util.Date;

public class HelloWorld {
    public String test(String name, int age, Date date) {
        return String.format("Name: %s, Age: %s, Date: %s", name, age, date);
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
        OutputUtils.save(unloadedType, true);
    }
}
```

### @Argument

```java
import net.bytebuddy.implementation.bind.annotation.Argument;
import net.bytebuddy.implementation.bind.annotation.RuntimeType;
import net.bytebuddy.implementation.bind.annotation.This;
import sample.HelloWorld;

import java.util.Date;
import java.util.Formatter;

public class HardWorker {
    @RuntimeType
    public static String doWork(@This HelloWorld instance,
                                @Argument(0) String name,
                                @Argument(1) int age,
                                @Argument(2) Date date) {
        StringBuilder sb = new StringBuilder();
        Formatter fm = new Formatter(sb);
        fm.format("Instance: %s%n", instance);
        fm.format("Name    : %s%n", name);
        fm.format("Age     : %s%n", age);
        fm.format("Date    : %s%n", date);
        return sb.toString();
    }
}
```

### @AllArguments

```java
import net.bytebuddy.implementation.bind.annotation.AllArguments;
import net.bytebuddy.implementation.bind.annotation.RuntimeType;
import net.bytebuddy.implementation.bind.annotation.This;
import sample.HelloWorld;

import java.util.Arrays;
import java.util.Formatter;

public class HardWorker {
    @RuntimeType
    public static void doWork(@This HelloWorld instance,
                              @AllArguments Object[] args) {
        StringBuilder sb = new StringBuilder();
        Formatter fm = new Formatter(sb);
        fm.format("Instance: %s%n", instance);
        fm.format("AllArgs : %s%n", Arrays.toString(args));
        System.out.println(sb);
    }
}
```

## 注意事项

### 数组

带有 `@AllArguments` 注解的参数必须是**数组**类型。

Parameters that carry the `@AllArguments` annotation must be of an array type.

```java
import net.bytebuddy.implementation.bind.annotation.AllArguments;

public class HardWorker {
    // 注意：这里没有 @RuntimeType
    public static void doWork(@AllArguments Object allArgs) {
        System.out.println("This is doWork Method");
    }
}
```

替换成 `String` 类型：

```java
import net.bytebuddy.implementation.bind.annotation.AllArguments;

public class HardWorker {
    public static void doWork(@AllArguments String allArgs) {
        System.out.println("This is doWork Method");
    }
}
```

```text
java.lang.IllegalStateException:
Expected an array type for all argument annotation on
public void sample.HelloWorld.test(java.lang.String,int,java.util.Date)
```

### 类型兼容

**All source method parameters must be assignable to the array's component type.**
If this is not the case, the current target method is not considered as a candidate for being bound to the source method.

将 `@AllArguments Object[] AllArgs` 中的 `Object[]` 替换成 `String[]`，再次运行，会有如下错误：

```text
java.lang.IllegalArgumentException: None of [HardWorker.doWork(Callable,String[]) ] allows for delegation from HelloWorld.test(String,int,Date)
```

原因是：`test()` 方法的第三个参数是 `Date` 类型，不能转换成 `String[]` 的参数。

