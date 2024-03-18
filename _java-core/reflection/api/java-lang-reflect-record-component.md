---
title: "java.lang.reflect.RecordComponent"
sequence: "108"
---

```text
                                      ┌─── name ───┼─── getName()
                                      │
                   ┌─── basic ────────┤            ┌─── getType()
                   │                  │            │
                   │                  └─── type ───┼─── getGenericType()
                   │                               │
                   │                               └─── getGenericSignature()
                   │
                   ├─── class ────────┼─── getDeclaringRecord()
RecordComponent ───┤
                   ├─── method ───────┼─── getAccessor()
                   │
                   │
                   │                  ┌─── getAnnotatedType()
                   │                  │
                   │                  ├─── getAnnotation(Class<T> annotationClass)
                   └─── annotation ───┤
                                      ├─── getAnnotations()
                                      │
                                      └─── getDeclaredAnnotations()
```
