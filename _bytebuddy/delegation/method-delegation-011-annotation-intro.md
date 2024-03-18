---
title: "Method Delegation: Annotation"
sequence: "111"
---

In reality, the `MethodDelegation` implementation works with **annotations**
where a parameter's annotation decides what value should be assigned to it.

However, if no annotation is found, Byte Buddy treats a parameter as if it was annotated with `@Argument`.

This `@Argument` annotation causes Byte Buddy to assign the `n`-th argument of the source method to the annotated
target.
When the annotation is not added explicitly, the value of `n` is set to the **annotated parameter's index**.
According to this rule, Byte Buddy treats

If the intercepted method does not declare at least two parameters or
if the annotated parameter types are not assignable from the instrumented method's parameter types,
the interceptor method in question is discarded.

> 从数量和类型，两方面考虑

```text
Annotation: source method --> 传递信息 --> target method
```

- @RuntimeType
- class
    - @Origin
- instance
    - @Default
    - @This
    - @Super
- method
    - @Origin
    - @Argument
    - @AllArguments
    - @SuperMethod
- field
- invoke
    - @SuperCall
    - @DefaultCall

```text
                                                       ┌─── class ──────┼─── @Origin
                                                       │
                               ┌─── current class ─────┼─── instance ───┼─── @This
                               │                       │
                               │                       │                ┌─── @Argument
MethodDelegation Annotation ───┤                       └─── method ─────┤
                               │                                        └─── @AllArguments
                               │
                               └─── class hierarchy ───┼─── @Super
```

对于这些注解（`@Origin`、`@SuperCall` 等），要学什么呢？要理解这样的思路：

```text
问题（应用场景） --> 注解 --> 参数类型
```

- 注解，它是用来获取一定的资源的（this、字段、父类的方法），解决某一个问题
- 注解，是用来修饰方法的参数的，它到底是什么样的类型？

两个类：

- `LazyWorker` 类：不带有 `@RuntimeType` 注解
- `HardWorker` 类：带有 `@RuntimeType` 注解
