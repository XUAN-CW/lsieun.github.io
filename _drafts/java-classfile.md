---
title: "Java ClassFile"
image: /assets/images/java/classfile/java-class-file-cover.jpg
permalink: /java-classfile.html
---

A Java class file is a file containing Java bytecode that can be executed on the Java Virtual Machine (JVM).

## Attributes

{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/jvm/classfile/attributes/'" |
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

## Opcodes

{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/jvm/classfile/opcode/'" |
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

## Reference

- [Java Language and Virtual Machine Specifications](https://docs.oracle.com/javase/specs/index.html)
