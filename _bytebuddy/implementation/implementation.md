---
title: "Implementation"
sequence: "101"
---

Note that Byte Buddy only invokes each `Implementation`'s `prepare` and `appender` methods a single time
during the creation process of any class.
This is guaranteed no matter how many times an implementation is registered for use in a class's creation.
This way, an `Implementation` can avoid to verify if a field or method is already defined.

> Implementation 的 prepare 和 appender 方法只会调用一次

In the process, Byte Buddy compares `Implementation`s instances by their `hashCode` and `equals` methods.
In general, any class that is used by Byte Buddy should provide meaningful implementations of these methods.

> ByteBuddy 会根据 hashCode 和 equals 方法进行判断，因此这两个方法要提供一个“合理”的实现。

The fact that enumerations come with such implementations per definition is another good reason for their use.

> 我猜测，这里应该是讲，使用 enum 是代替 hashCode 和 equals 的一个好方法

```java
import net.bytebuddy.ByteBuddy;
import net.bytebuddy.description.modifier.Visibility;
import net.bytebuddy.dynamic.DynamicType;
import net.bytebuddy.implementation.MethodDelegation;

public class HelloWorldSubClass {
    public static void main(String[] args) throws Exception {
        // 第一步，准备参数
        String className = "sample.HelloWorld";


        // 第二步，生成类
        ByteBuddy byteBuddy = new ByteBuddy();
        DynamicType.Builder<?> builder = byteBuddy.subclass(Object.class)
                .modifiers(Visibility.PUBLIC)
                .name(className);

        MethodDelegation methodDelegation = MethodDelegation.to(HardWorker.class);

        builder = builder.defineMethod("test1", String.class, Visibility.PUBLIC)
                .withParameters(String.class, int.class)
                .intercept(methodDelegation); // 第一次使用

        builder = builder.defineMethod("test2", String.class, Visibility.PUBLIC)
                .withParameters(String.class, int.class)
                .intercept(methodDelegation); // 第二次使用


        // 第三步，输出结果
        DynamicType.Unloaded<?> unloadedType = builder.make();
        OutputUtils.save(unloadedType);
    }
}
```



## Implementation

```java
public interface Implementation extends InstrumentedType.Prepareable {
    ByteCodeAppender appender(Target implementationTarget);
}
```

```java
public interface InstrumentedType extends TypeDescription {
    interface Prepareable {
        InstrumentedType prepare(InstrumentedType instrumentedType);
    }
}
```

## Implementation.Composable

```java
public interface Implementation extends InstrumentedType.Prepareable {
    interface Composable extends Implementation {
        Implementation andThen(Implementation implementation);

        Composable andThen(Composable implementation);
    }
}
```

## Implementation.Target

```java
public interface Implementation extends InstrumentedType.Prepareable {
    interface Target {
        TypeDescription getInstrumentedType();
        TypeDefinition getOriginType();

        SpecialMethodInvocation invokeSuper(MethodDescription.SignatureToken token);
        SpecialMethodInvocation invokeDefault(MethodDescription.SignatureToken token);
        SpecialMethodInvocation invokeDefault(MethodDescription.SignatureToken token, TypeDescription targetType);
        SpecialMethodInvocation invokeDominant(MethodDescription.SignatureToken token);
    }
}
```

## Implementation.Simple

```java
public interface Implementation extends InstrumentedType.Prepareable {
    class Simple implements Implementation {
        private final ByteCodeAppender byteCodeAppender;

        public Simple(ByteCodeAppender... byteCodeAppender) {
            this.byteCodeAppender = new ByteCodeAppender.Compound(byteCodeAppender);
        }

        public Simple(StackManipulation... stackManipulation) {
            byteCodeAppender = new ByteCodeAppender.Simple(stackManipulation);
        }

        public InstrumentedType prepare(InstrumentedType instrumentedType) {
            return instrumentedType;
        }

        public ByteCodeAppender appender(Target implementationTarget) {
            return byteCodeAppender;
        }
    }
}
```
