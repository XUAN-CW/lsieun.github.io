---
title: "@Advice.Enter：从 MethodEnter 向 MethodExit 传递数据"
sequence: "109"
---

The annotated parameter should be mapped to the value
that is returned by the advice method
that is annotated by `Advice.OnMethodEnter`.

Note: This annotation must only be used within **an exit advice** and is only meaningful in combination with **an enter advice**.

## @Advice.Enter

```java
@Retention(RetentionPolicy.RUNTIME)
@java.lang.annotation.Target(ElementType.PARAMETER)
public @interface Enter {
    boolean readOnly() default true;
    Assigner.Typing typing() default Assigner.Typing.STATIC;
}
```

## 示例

### HelloWorld

```java
public class HelloWorld {
    public void test() {
        System.out.println("Hello World");
    }
}
```

### Expert

```java
import net.bytebuddy.asm.Advice;

public class Expert {
    @Advice.OnMethodEnter
    public static String methodEnter() {
        String sharedSecrets = "Tomorrow is Sunday!";
        System.out.println("Hello Method Enter");
        return sharedSecrets;
    }

    @Advice.OnMethodExit
    public static void methodExit(
            @Advice.Enter String sharedSecrets
    ) {
        System.out.println("Hello Method Exit");
        System.out.println(sharedSecrets);
    }
}
```

### Rebase

```java
import net.bytebuddy.ByteBuddy;
import net.bytebuddy.asm.Advice;
import net.bytebuddy.dynamic.DynamicType;
import net.bytebuddy.matcher.ElementMatchers;

public class HelloWorldRedefine {
    public static void main(String[] args) throws Exception {
        // 第一步，准备参数
        String className = "sample.HelloWorld";
        Class<?> clazz = Class.forName(className);


        // 第二步，生成类
        ByteBuddy byteBuddy = new ByteBuddy();
        DynamicType.Builder<?> builder = byteBuddy.redefine(clazz);

        builder = builder.visit(
                Advice.to(Expert.class).on(ElementMatchers.isMethod())
        );


        // 第三步，输出结果
        DynamicType.Unloaded<?> unloadedType = builder.make();
        OutputUtils.save(unloadedType, true);
    }
}
```

### Run

```java
public class HelloWorldRun {
    public static void main(String[] args) throws Exception {
        String className = "sample.HelloWorld";
        InvokeUtils.invokeAllMethods(className);
    }
}
```

