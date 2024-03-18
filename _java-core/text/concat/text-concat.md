---
title: "String Concat"
sequence: "101"
---

## JDK: String.join

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {

    public static String join(CharSequence delimiter, CharSequence... elements) {
        // Number of elements not likely worth Arrays.stream overhead.
        StringJoiner joiner = new StringJoiner(delimiter);
        for (CharSequence cs: elements) {
            joiner.add(cs);
        }
        return joiner.toString();
    }
    
    public static String join(CharSequence delimiter,
                              Iterable<? extends CharSequence> elements) {
        StringJoiner joiner = new StringJoiner(delimiter);
        for (CharSequence cs: elements) {
            joiner.add(cs);
        }
        return joiner.toString();
    }
}
```

示例一：

```java
public class TextJoin {
    public static void main(String[] args) {
        String message = String.join("-", "Java", "is", "cool");
        System.out.println(message);
    }
}
```

```text
Java-is-cool
```

示例二：

```java
import java.util.List;

public class TextJoin {
    public static void main(String[] args) {
        List<String> strings = List.of("Java", "is", "cool");
        String message = String.join(" ", strings);
        System.out.println(message);
    }
}
```

```text
Java is cool
```
