---
title: "Java Reflection"
sequence: "java-reflection"
---

## Basic

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/reflection/basic/'" |
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

## Feature

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/reflection/feature/'" |
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

## Access

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/reflection/access/'" |
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
where_exp: "item", "item.url contains '/java-core/reflection/advanced/'" |
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

## API

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/reflection/api/'" |
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

- deep reflection
  - private fields or nonpublic methods
  - setAccessible

## Reference

Oracle

- [Trail: The Reflection API](https://docs.oracle.com/javase/tutorial/reflect/)

Github

- [eugenp/tutorials](https://github.com/eugenp/tutorials/tree/master/core-java-modules/core-java-reflection)

jenkov

- [Java Reflection Tutorial](http://tutorials.jenkov.com/java-reflection/index.html)


