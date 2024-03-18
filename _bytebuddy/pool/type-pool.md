---
title: "TypePool"
sequence: "101"
---

```text
TypePool ---> TypePool.Resolution ---> TypeDescription
```

## TypePool

```java
public interface TypePool {
    Resolution describe(String name);
    void clear();
}
```

## TypePool.Resolution

```java
public interface TypePool {
    interface Resolution {
        boolean isResolved();

        TypeDescription resolve();
    }
}
```

## TypePool.Default

```java
public interface TypePool {
    class Default extends AbstractBase.Hierarchical {
        public static TypePool ofSystemLoader() {
            return of(ClassFileLocator.ForClassLoader.ofSystemLoader());
        }

        public static TypePool ofPlatformLoader() {
            return of(ClassFileLocator.ForClassLoader.ofPlatformLoader());
        }

        public static TypePool ofBootLoader() {
            return of(ClassFileLocator.ForClassLoader.ofBootLoader());
        }

        public static TypePool of(@MaybeNull ClassLoader classLoader) {
            return of(ClassFileLocator.ForClassLoader.of(classLoader));
        }

        public static TypePool of(ClassFileLocator classFileLocator) {
            return new Default(new CacheProvider.Simple(), classFileLocator, ReaderMode.FAST);
        }
    }
}
```

## 总结

```text
            ┌─── Empty
            │
            │                                                              ┌─── ofSystemLoader()
            │                                                              │
            │                                                              ├─── ofPlatformLoader()
            │                                                              │
            │                                         ┌─── Default ────────┼─── ofBootLoader()
TypePool ───┤                                         │                    │
            │                                         │                    ├─── of(ClassLoader classLoader)
            │                                         │                    │
            │                                         │                    └─── of(ClassFileLocator classFileLocator)
            │                                         │
            │                                         ├─── LazyFacade
            │                                         │
            │                                         │                    ┌─── of(ClassLoader classLoader)
            └─── AbstractBase ───┼─── Hierarchical ───┤                    │
                                                      │                    ├─── of(ClassLoader classLoader, TypePool parent)
                                                      │                    │
                                                      ├─── ClassLoading ───┼─── ofSystemLoader()
                                                      │                    │
                                                      │                    ├─── ofPlatformLoader()
                                                      │                    │
                                                      │                    └─── ofBootLoader()
                                                      │
                                                      └─── Explicit
```
