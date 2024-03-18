---
title: "SuperMethodCall"
sequence: "104"
---

## SuperMethodCall

```java

```

## SuperMethodCall

```java

```

## Examples

```java
public class Parent {
    public void test() {
        System.out.println("test method from Parent");
    }
}
```

```java
public class HelloWorld extends Parent {
    public void test() {
        super.test();
    }
}
```

```java
import net.bytebuddy.ByteBuddy;
import net.bytebuddy.description.modifier.Visibility;
import net.bytebuddy.dynamic.DynamicType;
import net.bytebuddy.implementation.SuperMethodCall;
import sample.Parent;

public class HelloWorldGenerate {
    public static void main(String[] args) throws Exception {
        // 第一步，准备参数
        String className = "sample.HelloWorld";


        // 第二步，生成类
        ByteBuddy byteBuddy = new ByteBuddy();
        DynamicType.Builder<?> builder = byteBuddy.subclass(Parent.class)
                .name(className);

        builder = builder.defineMethod("test", void.class, Visibility.PUBLIC)
                .intercept(SuperMethodCall.INSTANCE);


        // 第三步，输出结果
        DynamicType.Unloaded<?> unloadedType = builder.make();
        OutputUtils.save(unloadedType);
    }
}
```

