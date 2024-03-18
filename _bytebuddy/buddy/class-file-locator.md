---
title: "ClassFileLocator"
sequence: "101"
---

## ClassFileLocator.ForJarFile

```java
import net.bytebuddy.dynamic.ClassFileLocator;

import java.io.File;
import java.io.IOException;

public class HelloWorldAnalysis {
    public static void main(String[] args) throws IOException {
        String jarPath = "C:\\Users\\1\\.m2\\repository\\com\\alibaba\\fastjson\\1.2.37\\fastjson-1.2.37.jar";

        try (
                ClassFileLocator jarFileLocator = ClassFileLocator.ForJarFile.of(new File(jarPath));
        ) {
            ClassFileLocator.Resolution resolution = jarFileLocator.locate("com.alibaba.fastjson.JSON");
            byte[] bytes = resolution.resolve();
            System.out.println(bytes.length);
        }

    }
}
```

## ClassFileLocator.ForFolder

```java
import net.bytebuddy.dynamic.ClassFileLocator;

import java.io.File;
import java.io.IOException;

public class HelloWorldAnalysis {
    public static void main(String[] args) throws IOException {
        String filepath = "D:\\workspace\\git-repo\\learn-byte-buddy\\target\\classes";
        String className = "lsieun.buddy.delegation.LazyWorker";

        try (
                ClassFileLocator folderLocator = new ClassFileLocator.ForFolder(new File(filepath));
        ) {
            ClassFileLocator.Resolution resolution = folderLocator.locate(className);
            byte[] bytes = resolution.resolve();
            System.out.println(bytes.length);
        }

    }
}
```
