---
title: "ClassFileLocator"
sequence: "103"
---

## 概览

`ClassFileLocator` 是一个接口，位于 `net.bytebuddy.dynamic` 包。

`ClassFileLocator` 的作用是获取 `byte[]`：由 `ClassFileLocator` 获取一个 `ClassFileLocator.Resolution`，再进一步得到 `byte[]`。

```text
ClassFileLocator ---> ClassFileLocator.Resolution ---> byte[]
```

从具体的实现来说，它有不同的实现：

{:refdef: style="text-align: center;"}
![](/assets/images/bytebuddy/class-file-locator-related-classes.png)
{:refdef}

## ClassFileLocator

```java
public interface ClassFileLocator extends Closeable {
    Resolution locate(String name) throws IOException;
}
```

## ClassFileLocator.Resolution

ClassFileLocator.Resolution

```java
public interface ClassFileLocator extends Closeable {
    interface Resolution {
        boolean isResolved();

        byte[] resolve();
    }
}
```

```java
public interface ClassFileLocator extends Closeable {
    interface Resolution {
        class Explicit implements Resolution {
            private final byte[] binaryRepresentation;

            public Explicit(byte[] binaryRepresentation) {
                this.binaryRepresentation = binaryRepresentation;
            }

            public boolean isResolved() {
                return true;
            }

            public byte[] resolve() {
                return binaryRepresentation;
            }
        }
    }
}
```



## ClassFileLocator.ForClassLoader

### 工作原理

```java
public interface ClassFileLocator extends Closeable {
    String CLASS_FILE_EXTENSION = ".class";

    class ForClassLoader implements ClassFileLocator {
        private final ClassLoader classLoader;

        protected ForClassLoader(ClassLoader classLoader) {
            this.classLoader = classLoader;
        }

        public Resolution locate(String name) throws IOException {
            return locate(classLoader, name);
        }

        public void close() {
            /* do nothing */
        }

        protected static Resolution locate(ClassLoader classLoader, String name) throws IOException {
            InputStream inputStream = classLoader.getResourceAsStream(name.replace('.', '/') + CLASS_FILE_EXTENSION);
            if (inputStream != null) {
                try {
                    return new Resolution.Explicit(StreamDrainer.DEFAULT.drain(inputStream));
                } finally {
                    inputStream.close();
                }
            } else {
                return new Resolution.Illegal(name);
            }
        }
    }
}
```

### 静态方法

#### ClassFileLocator

```java
public interface ClassFileLocator extends Closeable {
    class ForClassLoader implements ClassFileLocator {
        public static ClassFileLocator ofSystemLoader() {
            return new ForClassLoader(ClassLoader.getSystemClassLoader());
        }

        public static ClassFileLocator ofPlatformLoader() {
            return of(ClassLoader.getSystemClassLoader().getParent());
        }

        public static ClassFileLocator ofBootLoader() {
            return new ForClassLoader(BOOT_LOADER_PROXY);
        }
    }
}
```

#### byte[]

```java
public interface ClassFileLocator extends Closeable {
    class ForClassLoader implements ClassFileLocator {
        public static byte[] read(Class<?> type) {
            try {
                ClassLoader classLoader = type.getClassLoader();
                return locate(classLoader == null
                        ? BOOT_LOADER_PROXY
                        : classLoader, TypeDescription.ForLoadedType.getName(type)).resolve();
            } catch (IOException exception) {
                throw new IllegalStateException("Cannot read class file for " + type, exception);
            }
        }

        public static Map<Class<?>, byte[]> read(Class<?>... type) {
            return read(Arrays.asList(type));
        }

        public static Map<Class<?>, byte[]> read(Collection<? extends Class<?>> types) {
            Map<Class<?>, byte[]> result = new HashMap<Class<?>, byte[]>();
            for (Class<?> type : types) {
                result.put(type, read(type));
            }
            return result;
        }

        public static Map<String, byte[]> readToNames(Class<?>... type) {
            return readToNames(Arrays.asList(type));
        }

        public static Map<String, byte[]> readToNames(Collection<? extends Class<?>> types) {
            Map<String, byte[]> result = new HashMap<String, byte[]>();
            for (Class<?> type : types) {
                result.put(type.getName(), read(type));
            }
            return result;
        }
    }
}
```

## ClassFileLocator.ForJarFile

### 工作原理

```java
public interface ClassFileLocator extends Closeable {
    class ForJarFile implements ClassFileLocator {
        private final JarFile jarFile;

        public ForJarFile(JarFile jarFile) {
            this.jarFile = jarFile;
        }

        public Resolution locate(String name) throws IOException {
            ZipEntry zipEntry = jarFile.getEntry(name.replace('.', '/') + CLASS_FILE_EXTENSION);
            if (zipEntry == null) {
                return new Resolution.Illegal(name);
            } else {
                InputStream inputStream = jarFile.getInputStream(zipEntry);
                try {
                    return new Resolution.Explicit(StreamDrainer.DEFAULT.drain(inputStream));
                } finally {
                    inputStream.close();
                }
            }
        }

        public void close() throws IOException {
            jarFile.close();
        }
    }
}
```

### 静态方法

```java
public interface ClassFileLocator extends Closeable {
    class ForJarFile implements ClassFileLocator {
        public static ClassFileLocator of(File file) throws IOException {
            return new ForJarFile(new JarFile(file));
        }

        public static ClassFileLocator ofClassPath() throws IOException {
            return ofClassPath(System.getProperty("java.class.path"));
        }

        public static ClassFileLocator ofClassPath(String classPath) throws IOException {
            List<ClassFileLocator> classFileLocators = new ArrayList<ClassFileLocator>();
            for (String element : Pattern.compile(System.getProperty("path.separator"), Pattern.LITERAL).split(classPath)) {
                File file = new File(element);
                if (file.isDirectory()) {
                    classFileLocators.add(new ForFolder(file));
                } else if (file.isFile()) {
                    classFileLocators.add(of(file));
                }
            }
            return new Compound(classFileLocators);
        }

        public static ClassFileLocator ofRuntimeJar() throws IOException {
            String javaHome = System.getProperty("java.home").replace('\\', '/');
            File runtimeJar = null;
            for (String location : RUNTIME_LOCATIONS) {
                File candidate = new File(javaHome, location);
                if (candidate.isFile()) {
                    runtimeJar = candidate;
                    break;
                }
            }
            if (runtimeJar == null) {
                throw new IllegalStateException("Runtime jar does not exist in " + javaHome + " for any of " + RUNTIME_LOCATIONS);
            }
            return of(runtimeJar);
        }
    }
}
```

## ClassFileLocator.ForInstrumentation

```java
public interface ClassFileLocator extends Closeable {
    class ForInstrumentation implements ClassFileLocator {
        private final Instrumentation instrumentation;
        private final ClassLoadingDelegate classLoadingDelegate;

        public ForInstrumentation(Instrumentation instrumentation, @MaybeNull ClassLoader classLoader) {
            this(instrumentation, ClassLoadingDelegate.Default.of(classLoader));
        }

        public ForInstrumentation(Instrumentation instrumentation, ClassLoadingDelegate classLoadingDelegate) {
            if (!DISPATCHER.isRetransformClassesSupported(instrumentation)) {
                throw new IllegalArgumentException(instrumentation + " does not support retransformation");
            }
            this.instrumentation = instrumentation;
            this.classLoadingDelegate = classLoadingDelegate;
        }

        public Resolution locate(String name) {
            try {
                ExtractionClassFileTransformer classFileTransformer = new ExtractionClassFileTransformer(classLoadingDelegate.getClassLoader(), name);
                DISPATCHER.addTransformer(instrumentation, classFileTransformer, true);
                try {
                    DISPATCHER.retransformClasses(instrumentation, new Class<?>[]{classLoadingDelegate.locate(name)});
                    byte[] binaryRepresentation = classFileTransformer.getBinaryRepresentation();
                    return binaryRepresentation == null
                            ? new Resolution.Illegal(name)
                            : new Resolution.Explicit(binaryRepresentation);
                } finally {
                    instrumentation.removeTransformer(classFileTransformer);
                }
            } catch (RuntimeException exception) {
                throw exception;
            } catch (Exception ignored) {
                return new Resolution.Illegal(name);
            }
        }
    }
}
```

## 总结

本文内容总结如下：

- 第一点，从整体上来说，`ClassFileLocator` 的作用是获取 `byte[]`。起点是 `ClassFileLocator`，终点是 `byte[]`。
- 第二点，从使用的角度来说，根据具体的场景，选择合适的 `ClassFileLocator` 实现类。

```text
                                     ┌─── none ──────────┼─── NoOp
                                     │
                                     ├─── byte[] ────────┼─── Simple
                                     │
                                     │                   ┌─── ForClassLoader
                                     │                   │
                                     ├─── classloader ───┼─── ForModule
                                     │                   │
                    ┌─── single ─────┤                   └─── ForUrl
                    │                │
                    │                │                   ┌─── ForModuleFile
                    │                │                   │
                    │                ├─── file ──────────┼─── ForJarFile
ClassFileLocator ───┤                │                   │
                    │                │                   └─── ForFolder
                    │                │
                    │                └─── agent ─────────┼─── ForInstrumentation
                    │
                    │                ┌─── PackageDiscriminating
                    └─── multiple ───┤
                                     └─── Compound
```

```text
                                     ┌─── none ──────────┼─── NoOp
                                     │
                                     │                                  ┌─── of(String typeName, byte[] binaryRepresentation)
                                     │                                  │
                                     │                                  ├─── of(DynamicType dynamicType)
                                     ├─── byte[] ────────┼─── Simple ───┤
                                     │                                  ├─── of(Map<TypeDescription, byte[]> binaryRepresentations)
                                     │                                  │
                                     │                                  └─── ofResources(Map<String, byte[]> binaryRepresentations)
                                     │
                                     │                                                       ┌─── ofSystemLoader()
                                     │                                                       │
                                     │                                                       ├─── ofPlatformLoader()
                                     │                                          ┌─── of ─────┤
                                     │                                          │            ├─── ofBootLoader()
                                     │                                          │            │
                                     │                                          │            └─── of(ClassLoader classLoader)
                                     │                   ┌─── ForClassLoader ───┤
                                     │                   │                      │            ┌─── read(Class<?> type)
                                     │                   │                      │            │
                                     │                   │                      │            ├─── read(Class<?>... type)
                                     │                   │                      │            │
                                     │                   │                      └─── read ───┼─── read(Collection<? extends Class<?>> types)
                                     │                   │                                   │
                                     ├─── classloader ───┤                                   ├─── readToNames(Class<?>... type)
                                     │                   │                                   │
                                     │                   │                                   └─── readToNames(Collection<? extends Class<?>> types)
                                     │                   │
                    ┌─── single ─────┤                   │                      ┌─── ofBootLayer()
                    │                │                   ├─── ForModule ────────┤
                    │                │                   │                      └─── of(JavaModule module)
                    │                │                   │
                    │                │                   └─── ForUrl
                    │                │
                    │                │                                         ┌─── of(File file)
                    │                │                                         │
                    │                │                                         ├─── ofClassPath()
                    │                │                   ┌─── ForJarFile ──────┤
                    │                │                   │                     ├─── ofClassPath(String classPath)
                    │                │                   │                     │
                    │                │                   │                     └─── ofRuntimeJar()
                    │                │                   │
                    │                │                   │                     ┌─── ofBootPath()
                    │                │                   │                     │
ClassFileLocator ───┤                │                   │                     ├─── ofBootPath(File bootPath)
                    │                ├─── file ──────────┤                     │
                    │                │                   │                     ├─── ofModulePath()
                    │                │                   ├─── ForModuleFile ───┤
                    │                │                   │                     ├─── ofModulePath(String modulePath)
                    │                │                   │                     │
                    │                │                   │                     ├─── ofModulePath(String modulePath, String baseFolder)
                    │                │                   │                     │
                    │                │                   │                     └─── of(File file)
                    │                │                   │
                    │                │                   └─── ForFolder
                    │                │
                    │                │                                              ┌─── fromInstalledAgent(ClassLoader classLoader)
                    │                └─── agent ─────────┼─── ForInstrumentation ───┤
                    │                                                               └─── of(Instrumentation instrumentation, Class<?> type)
                    │
                    │                ┌─── PackageDiscriminating
                    └─── multiple ───┤
                                     └─── Compound
```

