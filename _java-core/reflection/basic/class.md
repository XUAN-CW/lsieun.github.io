---
title: "Class"
sequence: "103"
---

## Unique Class

No matter how many objects of a class you create in your program,
Java creates only one `Class` object for each class loaded by **a class loader** in a JVM from **one module**.

In a JVM, a class is uniquely identified by **its fully qualified name**, **its class loader**, and **its module**.
If two different class loaders load the same class,
the two loaded classes are considered two different classes,
and their objects are not compatible with each other.

## 获取 Class

You can get the reference to the `Class` object of a class in one of the followings ways:

- Using class literal
- Using the `getClass()` method of the `Object` class
- Using the `forName()` static method of the `Class` class

### Using Class Literals

A class literal is the class name or interface name followed by a dot and the word “class.” 

```text
Class<Test> testClass = Test.class;
```

You can also get the class object for **primitive data types** and
the keyword `void` using class literals as
`boolean.class`, `byte.class`, `char.class`, `short.class`, `int.class`,
`long.class`, `float.class`, `double.class`, and `void.class`.

Each wrapper class for these primitive data types has a static field named `TYPE`,
which has the reference to the class object of the primitive data type it represents.
Therefore, `int.class` and `Integer.TYPE` refer to the same class object,
and the expression `int.class == Integer.TYPE` evaluates to `true`.

### Object::getClass()

The `Object` class contains a `getClass()` method,
which returns the reference to the `Class` object of the class of the object.
This method is available in every class in Java
because every class in Java, explicitly or implicitly, inherits the `Object` class.
The method is declared `final`, so no descendant class can override it.

```text
Test testRef = new Test();
Class<?> testClass = testRef.getClass();
```

### Class::forName()

The `Class` class has a `forName()` static method,
which loads a class and returns the reference to its `Class` object.
It is an overloaded method.

```text
Class<?> forName(String className) throws ClassNotFoundException
Class<?> forName(String className, boolean initialize, ClassLoader loader) throws ClassNotFoundException

// Since Java 9
Class<?> forName(Module module, String className)
```

The `forName(String className)` method takes the fully qualified name of the class to be loaded.
It loads the class, initializes it, and returns the reference to its `Class` object.
If the class is already loaded, it simply returns the reference to the `Class` object of that class.

The `forName(String className, boolean initialize, ClassLoader loader)` method
gives you options to initialize or not to initialize the class when it is loaded,
and which class loader should load the class.
The first two versions of the method throw a `ClassNotFoundException` if the class could not be loaded.

The `forName(Module module, String className)` method loads the class
with the specified `className` in the specified module without initializing the loaded class.
If the class is not found, the method returns `null`.


The `forName(String className)` method **initializes the class** if it is not already initialized,
whereas **the use of a class literal does not initialize the class**.
When a class is initialized, all its static initializers are executed,
and all static fields are initialized.

```text
                                                      ┌─── getName()
                                                      │
                                                      ├─── getSimpleName()
                                     ┌─── name ───────┤
                                     │                ├─── getTypeName()
                 ┌─── class info ────┤                │
                 │                   │                └─── getCanonicalName()
                 │                   │
                 │                   └─── modifier ───┼─── getModifiers()
                 │
                 │                   ┌─── getFields()
                 │                   │
                 │                   ├─── getDeclaredFields()
                 ├─── field ─────────┤
                 │                   ├─── getField(String name)
                 │                   │
                 │                   └─── getDeclaredField(String name)
Class: member ───┤
                 │                   ┌─── getConstructors()
                 │                   │
                 │                   ├─── getDeclaredConstructors()
                 ├─── constructor ───┤
                 │                   ├─── getConstructor(Class<?>... parameterTypes)
                 │                   │
                 │                   └─── getDeclaredConstructor(Class<?>... parameterTypes)
                 │
                 │                   ┌─── getMethods()
                 │                   │
                 │                   ├─── getDeclaredMethods()
                 └─── method ────────┤
                                     ├─── getMethod(String name, Class<?>... parameterTypes)
                                     │
                                     └─── getDeclaredMethod(String name, Class<?>... parameterTypes)
```

```text
                                     ┌─── type parameter ───┼─── getTypeParameters()
                                     │
                  ┌─── generic ──────┼─── super ────────────┼─── getGenericSuperclass()
                  │                  │
                  │                  │                      ┌─── toString()
                  │                  └─── str ──────────────┤
                  │                                         └─── toGenericString()
                  │
                  │                  ┌─── type ────────┼─── isAnnotation()
Class: feature ───┤                  │
                  │                  │                                  ┌─── getAnnotation(Class<A> annotationClass)
                  │                  │                 ┌─── single ─────┤
                  │                  │                 │                └─── getDeclaredAnnotation(Class<A> annotationClass)
                  │                  │                 │
                  │                  │                 ├─── is ─────────┼─── isAnnotationPresent(Class<? extends Annotation> annotationClass)
                  │                  ├─── instance ────┤
                  └─── annotation ───┤                 │                ┌─── getAnnotationsByType(Class<A> annotationClass)
                                     │                 │                │
                                     │                 │                ├─── getDeclaredAnnotationsByType(Class<A> annotationClass)
                                     │                 └─── multiple ───┤
                                     │                                  ├─── getAnnotations()
                                     │                                  │
                                     │                                  └─── getDeclaredAnnotations()
                                     │
                                     │                 ┌─── getAnnotatedSuperclass()
                                     └─── hierarchy ───┤
                                                       └─── getAnnotatedInterfaces()
```

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
               │
Class: type ───┼─── hidden ───┼─── isHidden()
               │
               │                             ┌─── getDeclaredClasses()
               │              ┌─── outer ────┤
               │              │              └─── getClasses()
               │              │
               │              │                                          ┌─── isMemberClass()
               ├─── nested ───┤              ┌─── common ────────────────┤
               │              │              │                           └─── getDeclaringClass()
               │              │              │
               │              │              ├─── static nested class
               │              │              │
               │              └─── member ───┤                                                   ┌─── isLocalClass()
               │                             │                                                   │
               │                             │                                                   ├─── getEnclosingClass()
               │                             │                           ┌─── local class ───────┤
               │                             │                           │                       ├─── getEnclosingMethod()
               │                             └─── inner class ───────────┤                       │
               │                                                         │                       └─── getEnclosingConstructor()
               │                                                         │
               │                                                         └─── anonymous class ───┼─── isAnonymousClass()
               │
               │              ┌─── isPrimitive()
               └─── is ───────┤
                              └─── isSynthetic()
```


```text
                 ┌─── loader ─────┼─── getClassLoader()
                 │
                 │                ┌─── forName(String className)
                 │                │
                 ├─── load ───────┼─── forName(String name, boolean initialize, ClassLoader loader)
                 │                │
                 │                └─── forName(Module module, String name)
Class: loader ───┤
                 │                ┌─── getResourceAsStream(String name)
                 ├─── resource ───┤
                 │                └─── getResource(String name)
                 │
                 ├─── security ───┼─── getProtectionDomain()
                 │
                 └─── signer ─────┼─── getSigners()
```

```text
                   ┌─── new ────┼─── newInstance()
                   │
Class: instance ───┼─── is ─────┼─── isInstance(Object obj)
                   │
                   └─── cast ───┼─── cast(Object obj)
```

```text
                    ┌─── module ───────┼─── getModule()
                    │
                    │                  ┌─── getPackage()
                    ├─── package ──────┤
                    │                  └─── getPackageName()
                    │
                    │                  ┌─── getSuperclass()
                    ├─── super ────────┤
Class: hierarchy ───┤                  └─── getGenericSuperclass()
                    │
                    │                  ┌─── isInterface()
                    │                  │
                    ├─── interface ────┼─── getInterfaces()
                    │                  │
                    │                  └─── getGenericInterfaces()
                    │
                    │                  ┌─── isAssignableFrom(Class<?> cls)
                    └─── compatible ───┤
                                       └─── asSubclass(Class<U> clazz)
```

```text
                                       ┌─── descriptorString()
Class: classfile ───┼─── descriptor ───┤
                                       └─── describeConstable()
```

