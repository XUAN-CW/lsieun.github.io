---
title: "Method Delegation: @FieldValue"
sequence: "1115"
---

## @FieldValue

`@FieldValue`: This annotation locates a field in the instrumented type's class hierarchy
and injects the field's value into the annotated parameter.

If no visible field of a compatible type can be found for the annotated parameter, the target method is not bound.


```java
public class HelloWorld {
    private final String name;
    private final int age;

    public HelloWorld(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String test() {
        return String.format("Name: %s, Age: %s", name, age);
    }
}
```

```java
public class HelloWorldRun {
    public static void main(String[] args) throws Exception {
        String className = "sample.HelloWorld";
        InvokeUtils.invokeAllMethods(className);
    }
}
```

```java
import net.bytebuddy.implementation.bind.annotation.FieldValue;

public class LazyWorker {
    public static String test(@FieldValue("name") String name,
                              @FieldValue("age") int age) {
        String message = String.format("%s - %d", name, age);
        return "message from LazyWorker: " + message;
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
                MethodDelegation.to(LazyWorker.class)
        );


        // 第三步，输出结果
        DynamicType.Unloaded<?> unloadedType = builder.make();
        OutputUtils.save(unloadedType, true);
    }
}
```

## 当没有匹配的字段时

```java
import net.bytebuddy.implementation.bind.annotation.FieldValue;

import java.util.Date;

public class LazyWorker {
    public static String test(@FieldValue("name") String name,
                              @FieldValue("age") int age,
                              @FieldValue("date") Date date) {
        String message = String.format("%s - %d - %s", name, age, date);
        return "message from LazyWorker: " + message;
    }
}
```
