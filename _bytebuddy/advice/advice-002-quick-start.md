---
title: "Advice: 快速开始"
sequence: "102"
---

## 示例

### 预期目标

假如有一个 `HelloWorld` 类：

```java
public class HelloWorld {
    public void test() {
        System.out.println("Hello World");
    }
}
```

预期目标：方法进入时，打印“Method Enter”；方法退出时，打印“Method Exit”

```java
public class HelloWorld {
    public void test() {
        System.out.println(">>> Method Enter");
        System.out.println("Hello World");
        System.out.println("<<< Method Exit");
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

### Expert

```java
import net.bytebuddy.asm.Advice;

public class Expert {
    @Advice.OnMethodEnter
    public static void methodEnter() {
        System.out.println(">>> Method Enter");
    }

    @Advice.OnMethodExit
    public static void methodExit() {
        System.out.println("<<< Method Exit");
    }
}
```


### 编码实现

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
                Advice.to(Expert.class)
                        .on(ElementMatchers.named("test"))
        );


        // 第三步，输出结果
        DynamicType.Unloaded<?> unloadedType = builder.make();
        OutputUtils.save(unloadedType, true);
    }
}
```
