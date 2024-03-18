---
title: "java.lang.Class"
sequence: "102"
---

## Basic

```text
         ┌─── module ────────┼─── getModule()
         │
         │                   ┌─── getPackage()
         ├─── package ───────┤
         │                   └─── getPackageName()
         │
         │                   ┌─── getSuperclass()
         ├─── super ─────────┤
         │                   └─── getGenericSuperclass()
         │
         │                   ┌─── isInterface()
         │                   │
         ├─── interface ─────┼─── getInterfaces()
         │                   │
         │                   └─── getGenericInterfaces()
         │
         │                   ┌─── getName()
         │                   │
         │                   ├─── getSimpleName()
         ├─── name ──────────┤
         │                   ├─── getTypeName()
         │                   │
         │                   └─── getCanonicalName()
Class ───┤
         ├─── modifier ──────┼─── getModifiers()
         │
         │                   ┌─── getFields()
         │                   │
         │                   ├─── getField(String name)
         ├─── field ─────────┤
         │                   ├─── getDeclaredFields()
         │                   │
         │                   └─── getDeclaredField(String name)
         │
         │                   ┌─── getConstructors()
         │                   │
         │                   ├─── getConstructor(Class<?>... parameterTypes)
         ├─── constructor ───┤
         │                   ├─── getDeclaredConstructors()
         │                   │
         │                   └─── getDeclaredConstructor(Class<?>... parameterTypes)
         │
         │
         │                   ┌─── getMethods()
         │                   │
         │                   ├─── getMethod(String name, Class<?>... parameterTypes)
         └─── method ────────┤
                             ├─── getDeclaredMethods()
                             │
                             └─── getDeclaredMethod(String name, Class<?>... parameterTypes)
```

## Generic And Annotation

```text
                                     ┌─── getTypeParameters()
                                     │
                                     ├─── super ─────────────────┼─── getGenericSuperclass()
                  ┌─── generic ──────┤
                  │                  │
                  │                  │                           ┌─── toString()
                  │                  └─── str ───────────────────┤
                  │                                              └─── toGenericString()
                  │                  ┌─── isAnnotation()
                  │                  │
Class: feature ───┤                  ├─── getAnnotation(Class<A> annotationClass)
                  │                  │
                  │                  ├─── isAnnotationPresent(Class<? extends Annotation> annotationClass)
                  │                  │
                  │                  ├─── getAnnotationsByType(Class<A> annotationClass)
                  │                  │
                  │                  ├─── getAnnotations()
                  └─── annotation ───┤
                                     ├─── getDeclaredAnnotation(Class<A> annotationClass)
                                     │
                                     ├─── getDeclaredAnnotationsByType(Class<A> annotationClass)
                                     │
                                     ├─── getDeclaredAnnotations()
                                     │
                                     ├─── getAnnotatedSuperclass()
                                     │
                                     └─── getAnnotatedInterfaces()
```

## Type

```text
                              ┌─── isArray()
                              │
                              ├─── getComponentType()
               ┌─── array ────┤
               │              ├─── componentType()
               │              │
               │              └─── arrayType()
               │
               │              ┌─── isEnum()
               ├─── enum ─────┤
               │              └─── getEnumConstants()
               │
               │              ┌─── isRecord()
               ├─── record ───┤
               │              └─── getRecordComponents()
               │
               │              ┌─── getNestHost()
               │              │
               ├─── nest ─────┼─── isNestmateOf(Class<?> c)
               │              │
               │              └─── getNestMembers()
               │
               │              ┌─── isSealed()
               ├─── sealed ───┤
               │              └─── getPermittedSubclasses()
Class: type ───┤
               ├─── hidden ───┼─── isHidden()
               │
               │              ┌─── isAnonymousClass()
               │              │
               │              ├─── isLocalClass()
               │              │
               │              ├─── isMemberClass()
               │              │
               │              ├─── getDeclaringClass()
               │              │
               ├─── nested ───┼─── getEnclosingClass()
               │              │
               │              ├─── getEnclosingMethod()
               │              │
               │              ├─── getEnclosingConstructor()
               │              │
               │              ├─── getClasses()
               │              │
               │              └─── getDeclaredClasses()
               │
               │              ┌─── isPrimitive()
               └─── is ───────┤
                              └─── isSynthetic()
```

## ClassLoader

```text
                 ┌─── loader ─────┼─── getClassLoader()
                 │
                 │                ┌─── forName(String className)
                 ├─── load ───────┤
                 │                └─── forName(Module module, String name)
                 │
Class: loader ───┤                ┌─── getResourceAsStream(String name)
                 ├─── resource ───┤
                 │                └─── getResource(String name)
                 │
                 ├─── security ───┼─── getProtectionDomain()
                 │
                 └─── signer ─────┼─── getSigners()
```

## Instance

```text
                                    ┌─── newInstance()
                                    │
Class: instance ───┼─── instance ───┼─── isInstance(Object obj)
                                    │
                                    └─── cast(Object obj)
```

## Hierarchy

```text
                                       ┌─── isAssignableFrom(Class<?> cls)
Class: hierarchy ───┼─── compatible ───┤
                                       └─── asSubclass(Class<U> clazz)
```

## Class File

```text
                                       ┌─── descriptorString()
Class: classfile ───┼─── descriptor ───┤
                                       └─── describeConstable()
```



