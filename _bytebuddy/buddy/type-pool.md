---
title: "TypePool"
sequence: "101"
---

```java
import net.bytebuddy.description.field.FieldDescription;
import net.bytebuddy.description.field.FieldList;
import net.bytebuddy.description.type.TypeDescription;
import net.bytebuddy.dynamic.ClassFileLocator;
import net.bytebuddy.pool.TypePool;

import java.io.File;
import java.io.IOException;

public class HelloWorldAnalysis {
    public static void main(String[] args) throws IOException {
        String jarPath = "C:\\Users\\1\\.m2\\repository\\com\\alibaba\\fastjson\\1.2.37\\fastjson-1.2.37.jar";

        try (
                ClassFileLocator jarFileLocator = ClassFileLocator.ForJarFile.of(new File(jarPath));
                ClassFileLocator systemLocator = ClassFileLocator.ForClassLoader.ofSystemLoader();
                ClassFileLocator compoundLocator = new ClassFileLocator.Compound(jarFileLocator, systemLocator);
        ) {
            TypePool typePool = TypePool.Default.of(compoundLocator);
            TypeDescription typeDescription = typePool.describe("com.alibaba.fastjson.JSON").resolve();

            System.out.println(typeDescription);

            FieldList<FieldDescription.InDefinedShape> declaredFields = typeDescription.getDeclaredFields();
            for (FieldDescription field : declaredFields) {
                System.out.println(field);
            }
        }

    }
}
```

```java
import net.bytebuddy.ByteBuddy;
import net.bytebuddy.description.type.TypeDescription;
import net.bytebuddy.dynamic.ClassFileLocator;
import net.bytebuddy.dynamic.DynamicType;
import net.bytebuddy.pool.TypePool;

import java.io.File;

public class HelloWorldRedefine {
    public static void main(String[] args) throws Exception {
        // 第一步，准备参数
        String className = "com.alibaba.fastjson.JSON";
        String jarPath = "C:\\Users\\1\\.m2\\repository\\com\\alibaba\\fastjson\\1.2.37\\fastjson-1.2.37.jar";


        try (
                ClassFileLocator jarFileLocator = ClassFileLocator.ForJarFile.of(new File(jarPath));
                ClassFileLocator systemLocator = ClassFileLocator.ForClassLoader.ofSystemLoader();
                ClassFileLocator compoundLocator = new ClassFileLocator.Compound(jarFileLocator, systemLocator);
        ) {
            TypePool typePool = TypePool.Default.of(compoundLocator);
            TypeDescription typeDescription = typePool.describe(className).resolve();

            // 第二步，生成类
            ByteBuddy byteBuddy = new ByteBuddy();
            // 这里的重点是：使用了 redefine(TypeDescription type, ClassFileLocator classFileLocator) 方法
            DynamicType.Builder<?> builder = byteBuddy.redefine(typeDescription, compoundLocator);

            // 第三步，输出结果
            DynamicType.Unloaded<?> unloadedType = builder.make();
            OutputUtils.save(unloadedType, true);
        }
    }
}
```
