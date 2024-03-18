---
title: "Generic"
sequence: "java-generic"
---

## Basic

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/basic/'" |
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

## Array

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/generic-and-array/'" |
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

## ClassFile

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/generic-and-classfile/'" |
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

## Reflection

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/generic-and-reflection/'" |
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

## Annotation

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/generics-and-annotation/'" |
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

## JDK

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/jdk/'" |
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

## Subtype

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/subtype-relationship/'" |
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

## Theme

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/theme/'" |
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

## Type Parameter

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/type-parameter/'" |
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

## Type Argument

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/type-argument/'" |
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

## Type Erasure

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/generic/type-erasure/'" |
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

TODO：

- [ ] 父类是泛型，子类不是泛型

类似于：

```text
public class Child extends Parent<Integer> {

}
```

```text
                                                           ┌─── Generic Type
                                    ┌─── Container Type ───┤
                                    │                      └─── Parameterized Type
                                    │
                 ┌─── Design ───────┤                                             ┌─── Unbounded Type Parameter
                 │                  │                      ┌─── Type Parameter ───┤
                 │                  │                      │                      └─── Bounded Type Parameter
                 │                  └─── Payload Type ─────┤
                 │                                         │                      ┌─── Concrete Type Argument
                 │                                         └─── Type Argument ────┤
                 │                                                                └─── Wildcard
Java Generics ───┤
                 │                  ┌─── Diamond Syntax
                 ├─── Java File ────┤
                 │                  └─── Type Inference
                 │
                 ├─── Compiler ─────┼─── Type Erasure
                 │
                 └─── Class File
```

**The idea of generics represents the abstraction over types**. It is a very powerful concept that allows to develop abstract algorithms and data structures and to provide concrete types to operate on later.

> 泛型，最核心的思想就是对 type 进行抽象（abstraction），可以将 type 作为参数传递。

Interestingly, generics were not present in the early versions of Java and were added along the way only in Java 5 release.( 泛型是在 Java 5 引入的 ) And since then, it is fair to say that generics revolutionized the way Java programs are being written, delivering much stronger type guaranties and making code significantly safer.

Collections that have all elements of the same type are called **homogeneous**, while the collections that can have elements of potentially different types are called **heterogeneous** (or sometimes "mystery meat collections").



Use Case:

问题一：对于一个 `.class` 文件来说，它可以分成多个部分：Magic Number、Version、Constant Pool、Class Info、Fields、Methods 和 Attributes。那么，泛型 `<T>` 可以应用到哪些地方？

我的回答：

- Class Info，分成三个地方：this_class、super_class、interfaces
- Fields
- Methods，分成两种：一种是依赖于 Class 的，另一种是独立的

问题二：Generics 和 Collections 之间是什么样的关系呢？

我的回答：

- 从时间上来说，Collections 是在 Java 1.2 加入的，而 Generics 是在 Java 5 加入的，以前的 Collections 的代码需要经过重构才能支持泛型，而泛型在实现上也是不完全的，它采用了 Type Erase 的方式来实现对过去的代码的兼容性
- 从我现在的理解来说，Generics 是对 Type 的参数化，现在的 Collections 和 Generics 进行结合之后，就是对 Collections 内的 Class、Field 和 Methods 中的 Type 的进行一种有效的约束。

## Which language features are related to Java generics?

**Features for definition and use of generic types and methods**.

Java Generics support definition and use of generic types and methods. It provides language features for the following purposes:

- definition of a generic type
- definition of a generic method

---

- type parameters
    - type parameter bounds
- type arguments
    - wildcards
    - wildcard bounds
    - wildcard capture
- instantiation of a generic type = parameterized type
    - raw type
    - concrete instantiation
    - wildcard instantiation
- instantiation of a generic method
    - automatic type inference
    - explicit type argument specification



## 联想

Type Erasure 让我想起了《丑八怪 - 薛之谦》中的“如果剧本写好 谁比谁高贵”

## Reference

- [Oracle - Lesson: Generics](https://docs.oracle.com/javase/tutorial/java/generics/index.html)
- [Angelika Langer: Java Generics FAQs](http://www.angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html)
