---
title: "Java Unsafe"
image: /assets/images/java/unsafe/java-unsafe-cartoon.png
permalink: /java-unsafe.html
---

Java Unsafe

## Basic

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/sun-misc/'" |
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

- [lsieun/learn-java-unsafe](https://github.com/lsieun/learn-java-unsafe)

- [Guide to sun.misc.Unsafe](https://www.baeldung.com/java-unsafe)
- [`sun/misc/Unsafe.java`](https://hg.openjdk.java.net/jdk8/jdk8/jdk/file/tip/src/share/classes/sun/misc/Unsafe.java)
