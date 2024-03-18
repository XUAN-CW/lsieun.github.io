---
title: "java.lang.reflect.Constructor"
sequence: "105"
---

```text
               ┌─── class ────────┼─── getDeclaringClass()
               │
               ├─── name ─────────┼─── getName()
               │
               ├─── modifier ─────┼─── getModifiers()
               │
               │                  ┌─── getParameterCount()
               │                  │
               ├─── parameter ────┼─── getParameterTypes()
               │                  │
               │                  └─── getGenericParameterTypes()
               │
               │                  ┌─── getExceptionTypes()
               ├─── exception ────┤
               │                  └─── getGenericExceptionTypes()
               │
               ├─── generic ──────┼─── getTypeParameters()
               │
               │                  ┌─── getAnnotation(Class<T> annotationClass)
Constructor ───┤                  │
               │                  ├─── getDeclaredAnnotations()
               │                  │
               ├─── annotation ───┼─── getParameterAnnotations()
               │                  │
               │                  ├─── getAnnotatedReturnType()
               │                  │
               │                  └─── getAnnotatedReceiverType()
               │
               ├─── access ───────┼─── setAccessible(boolean flag)
               │
               │                  ┌─── toString()
               ├─── str ──────────┤
               │                  └─── toGenericString()
               │
               │                  ┌─── isVarArgs()
               ├─── is ───────────┤
               │                  └─── isSynthetic()
               │
               └─── instance ─────┼─── newInstance(Object ... initargs)
```
