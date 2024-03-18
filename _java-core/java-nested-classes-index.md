---
title: "Nested Classes"
sequence: "java-nested-class"
---

The Java programming language allows you to define a class within another class.
Such a class is called a **nested class** and is illustrated here:

```text
class OuterClass {
    ...
    class NestedClass {
        ...
    }
}
```

Terminology: Nested classes are divided into two categories: non-static and static.
Non-static nested classes are called **inner classes**.
Nested classes that are declared `static` are called **static nested classes**.

```text
class OuterClass {
    ...
    class InnerClass {
        ...
    }
    static class StaticNestedClass {
        ...
    }
}
```



There are two special kinds of **inner classes**: **local classes** and **anonymous classes**.

```text
                ┌─── static    : static nested class
                │
nested class ───┤                                       ┌─── normal
                │                                       │
                └─── non-static: inner class ───────────┤
                                                        │               ┌─── local class
                                                        └─── special ───┤
                                                                        └─── anonymous class
```

## access and modifier 

A nested class is a member of its enclosing class.
Non-static nested classes (inner classes) have access to other members of the enclosing class, even if they are declared `private`.
Static nested classes do not have access to other members of the enclosing class.

```text
                                                        ┌─── static nested class
                              ┌─── static member ───────┤
                              │                         └─── inner class
access ───┼─── outer class ───┤
                              │
                              └─── non-static member ───┼─── inner class
```

As a member of the `OuterClass`, a nested class can be declared `private`, `public`, `protected`, or package private.
(Recall that outer classes can only be declared `public` or package private.)

```text
                                 ┌─── public
            ┌─── outer class ────┤
            │                    └─── package private
            │
modifier ───┤                    ┌─── public
            │                    │
            │                    ├─── protected
            └─── nested class ───┤
                                 ├─── private
                                 │
                                 └─── package private
```

## Why Use Nested Classes?

Compelling reasons for using nested classes include the following:

- **It is a way of logically grouping classes that are only used in one place**:
  If a class is useful to only one other class, then it is logical to embed it in that class and keep the two together.
  Nesting such "helper classes" makes their package more streamlined.

- **It increases encapsulation**:
  Consider two top-level classes, A and B, where B needs access to members of A that would otherwise be declared `private`.
  By hiding class B within class A, A's members can be declared `private` and B can access them.
  In addition, B itself can be hidden from the outside world.

- **It can lead to more readable and maintainable code**:
  Nesting small classes within top-level classes places the code closer to where it is used.

## Content

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/nested/'" |
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

## References

- [Nested Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)
