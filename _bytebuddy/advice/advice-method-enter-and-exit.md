---
title: "Advice：方法进入和方法退出"
sequence: "141"
---

ByteBuddy inlines the bytecode of the advice code
and produces the instrumented code.

```java
package net.bytebuddy.asm;

public class Advice implements AsmVisitorWrapper.ForDeclaredMethods.MethodVisitorWrapper, Implementation {
}
```

```text
                                                   ┌─── AbstractBase
                                                   │
                  ┌─── AsmVisitorWrapper ──────────┼─── ForDeclaredFields ────┼─── FieldVisitorWrapper
                  │                                │
                  │                                └─── ForDeclaredMethods ───┼─── MethodVisitorWrapper
                  │
                  ├─── Advice
asm ──────────────┤
                  ├─── MemberRemoval
                  │
                  │
                  │                                ┌─── ForField
                  └─── MemberAttributeExtension ───┤
                                                   └─── ForMethod
```

- `DynamicType.Builder.build()` 方法接收的是 `AsmVisitorWrapper` 类型的值，返回是 `DynamicType.Builder` 类型。
- `Advice.to()` 方法返回的是 `Advice` 类型。
- `Advice.on()` 方法返回的是 `AsmVisitorWrapper.ForDeclaredMethods` 类型，它又是 `AsmVisitorWrapper` 的子类型。



## Advice 的要求

对于 Advice 的要求：

- Annotation（注解）：必须带有 `@Advice.OnMethodEnter`，这样 ByteBuddy 才能知道是哪一个方法。
- Access Flag（访问标识）：必须是 `static` 方法；否则，会失败。
- Instruction（方法代码）：代码逻辑，必须是“有效”的代码。

`@Advice.OnMethodEnter`: 

- Any class must declare at most one method with this annotation.
- The annotated method must be static.
- When instrumenting constructors, the this values can only be accessed for writing fields but not for reading fields or invoking methods.

如果没有 `@Advice.OnMethodEnter` 等注解，则会提示：

```text
java.lang.IllegalArgumentException: No advice defined by class lsieun.buddy.advice.Expert
```

如果不是 `static` 方法，会提示如下错误信息：

```text
java.lang.IllegalStateException: Advice for public void lsieun.buddy.advice.Expert.methodEnter() is not static
```

如果方法体内的代码，不是“有效”的代码，例如调用 `private` 方法：

```java
import net.bytebuddy.asm.Advice;

public class Expert {
    @Advice.OnMethodEnter
    public static void methodEnter() {
        System.out.println("Method Enter");
        myPrivateMethod();
    }

    private static void myPrivateMethod() {
        System.out.println("Hello ByteBuddy");
    }
}
```

有效的代码：

```java
import net.bytebuddy.asm.Advice;

import java.util.logging.Level;
import java.util.logging.Logger;

public class Expert {
    public static Logger logger = Logger.getLogger(Expert.class.getName());

    @Advice.OnMethodEnter
    public static void methodEnter() {
        System.out.println("Method Enter");
        logger.log(Level.INFO, "Hello ByteBuddy");
    }
}
```
