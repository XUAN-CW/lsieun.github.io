---
title: "Interface"
sequence: "103"
---

## 示例一

```java
public class HelloWorld implements Cloneable {
}
```

```java

import net.bytebuddy.ByteBuddy;
import net.bytebuddy.dynamic.DynamicType;

import java.io.File;

public class HelloWorldSubclass {
    public static void main(String[] args) throws Exception {
        String className = "sample.HelloWorld";

        ByteBuddy byteBuddy = new ByteBuddy();
        DynamicType.Builder<?> builder = byteBuddy.subclass(Object.class)
                .name(className).implement(Cloneable.class);

        DynamicType.Unloaded<?> unloadedType = builder.make();

        File dirFile = FileUtils.getOutputDirectory();
        unloadedType.saveIn(dirFile);
    }
}
```

如果想实现两个接口：

```text
DynamicType.Builder<?> builder = byteBuddy.subclass(Object.class)
        .name(className).implement(Cloneable.class, Serializable.class);
```
