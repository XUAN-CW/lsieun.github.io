---
title: "Annotation"
sequence: "java-annotation"
---

## Basic

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/annotation/basic/'" |
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

## 定义注解

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/annotation/declare/'" |
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

## 使用注解

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/annotation/usage/'" |
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
where_exp: "item", "item.url contains '/java-core/annotation/reflection/'" |
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

## Advanced

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/annotation/advanced/'" |
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

- [JEP 277: Enhanced Deprecation](https://openjdk.java.net/jeps/277)
- [Get a Field's Annotations Using Reflection](https://www.baeldung.com/java-get-field-annotations)
- [Java Annotations and Java Reflection - Tutorial](https://www.vogella.com/tutorials/JavaAnnotations/article.html)
- [Java Reflection - Annotations](https://jenkov.com/tutorials/java-reflection/annotations.html)
