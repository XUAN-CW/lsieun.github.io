---
title: "Java Core"
image: /assets/images/java/core/learn-java.jpg
permalink: /java-core.html
---

Java Core covers the basic concept of Java programming language.

## Java Core

Basic:

- [JSL, JSR, JEP]({% link _java-core/glossary/jls-jsr-jep.md %})

Java Lang

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/java-lang/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

Basic Type:

- [Number]({% link _java-core/java-number-index.md %})
- [Text]({% link _java-core/java-text-index.md %})


Type:

- [Annotation]({% link _java-core/java-annotation-index.md %})
- [Enum]({% link _java-core/java-enum-index.md %})
- [Generic]({% link _java-core/java-generic-index.md %})
- [Interface]({% link _java-core/java-interface-index.md %})
- [Nested]({% link _java-core/java-nested-classes-index.md %})
- [Reflection]({% link _java-core/java-reflection-index.md %})
- [Sealed]({% link _java-core/java-sealed-index.md %})
- [Serialization]({% link _java-core/java-serialization-index.md %})

Utils:

- [Resource]({% link _java-core/resource-index.md %})
- [Properties]({% link _java-core/properties-index.md %})
- [Invoke]({% link _java-core/java-invoke-index.md %})


Glossary:

- [Glossary]({% link _java-core/glossary-index.md %})

## References

- [The Java Tutorials](https://docs.oracle.com/javase/tutorial/index.html)
    - Trails Covering the Basics
        - [Java Tutorials Learning Paths](https://docs.oracle.com/javase/tutorial/tutorialLearningPaths.html)
        - [Trail: Learning the Java Language](https://docs.oracle.com/javase/tutorial/java/index.html)
            - [Object-Oriented Programming Concepts](https://docs.oracle.com/javase/tutorial/java/concepts/index.html)
            - [Language Basics](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/index.html)
            - [Classes and Objects](https://docs.oracle.com/javase/tutorial/java/javaOO/index.html)
            - [Annotations](https://docs.oracle.com/javase/tutorial/java/annotations/index.html)
            - [Interfaces and Inheritance](https://docs.oracle.com/javase/tutorial/java/IandI/index.html)
            - [Numbers and Strings](https://docs.oracle.com/javase/tutorial/java/data/index.html)
            - [Generics](https://docs.oracle.com/javase/tutorial/java/generics/index.html)
            - [Packages](https://docs.oracle.com/javase/tutorial/java/package/index.html)
        - [Trail: Essential Java Classes](https://docs.oracle.com/javase/tutorial/essential/index.html)
            - [Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html)
            - [Basic I/O](https://docs.oracle.com/javase/tutorial/essential/io/index.html)
            - [Concurrency](https://docs.oracle.com/javase/tutorial/essential/concurrency/index.html)
            - [The Platform Environment](https://docs.oracle.com/javase/tutorial/essential/environment/index.html)
            - [Regular Expressions](https://docs.oracle.com/javase/tutorial/essential/regex/index.html)
        - [Trail: Collections](https://docs.oracle.com/javase/tutorial/collections/index.html)
            - [Introduction](https://docs.oracle.com/javase/tutorial/collections/intro/index.html)
            - [Interfaces](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html)
            - [Aggregate Operations](https://docs.oracle.com/javase/tutorial/collections/streams/index.html)
            - [Implementations](https://docs.oracle.com/javase/tutorial/collections/implementations/index.html)
            - [Algorithms](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html)
            - [Custom Implementations](https://docs.oracle.com/javase/tutorial/collections/custom-implementations/index.html)
            - [Interoperability](https://docs.oracle.com/javase/tutorial/collections/interoperability/index.html)
        - [Trail: Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html)
        - [Trail: Deployment](https://docs.oracle.com/javase/tutorial/deployment/index.html)
    - Specialized Trails and Lessons
        - [Custom Networking](https://docs.oracle.com/javase/tutorial/networking/index.html)
        - [The Extension Mechanism](https://docs.oracle.com/javase/tutorial/ext/index.html)
        - [Full-Screen Exclusive Mode API](https://docs.oracle.com/javase/tutorial/extra/fullscreen/index.html)
        - [Generics](https://docs.oracle.com/javase/tutorial/extra/generics/index.html)
        - [Internationalization](https://docs.oracle.com/javase/tutorial/i18n/index.html)
        - [JavaBeans](https://docs.oracle.com/javase/tutorial/javabeans/index.html)
        - [JAXB](https://docs.oracle.com/javase/tutorial/jaxb/index.html)
        - [JAXP](https://docs.oracle.com/javase/tutorial/jaxp/index.html)
        - [JDBC Database Access](https://docs.oracle.com/javase/tutorial/jdbc/index.html)
        - [JMX](https://docs.oracle.com/javase/tutorial/jmx/index.html)
        - [JNDI](https://docs.oracle.com/javase/tutorial/jndi/index.html)
        - [Reflection](https://docs.oracle.com/javase/tutorial/reflect/index.html)
        - [RMI](https://docs.oracle.com/javase/tutorial/rmi/index.html)
        - [Security](https://docs.oracle.com/javase/tutorial/security/index.html)
        - [Sockets Direct Protocol](https://docs.oracle.com/javase/tutorial/sdp/index.html)
        - [Sound](https://docs.oracle.com/javase/tutorial/sound/index.html)
        - [2D Graphics](https://docs.oracle.com/javase/tutorial/2d/index.html)
- [Java Platform Standard Edition 8 Documentation](https://docs.oracle.com/javase/8/docs/) ，这个页面有图，将 JDK、JRE、JMX 等内容分成了不同的小部分。
- [JDK Releases Matrix](https://www.java.com/releases/matrix/)
- [Java Language and Virtual Machine Specifications](https://docs.oracle.com/javase/specs/index.html)

- [JavaBeans Spec](https://www.oracle.com/java/technologies/javase/javabeans-spec.html)

OpenJDK

- [OpenJDK: src/share/classes](https://hg.openjdk.java.net/jdk8/jdk8/jdk/file/tip/src/share/classes)

- [IBM Developer](https://developer.ibm.com/)

JCP/JSR

- [Java Community Process](https://jcp.org/en/home/index)

JEPs

```text
https://openjdk.java.net/jeps/xxx
```

```text
https://openjdk.java.net/jeps/277
```
