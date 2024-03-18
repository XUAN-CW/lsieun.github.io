---
title: "Java Collection"
image: /assets/images/java/collection/java-collections-cover.png
permalink: /java-collection.html
---

Java Collection

{:refdef: style="text-align: center;"}
![](/assets/images/java/collection/java-collection-framework-hierarchy.webp)
{:refdef}

## Content

{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/collection/map/'" |
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

- [Collection Framework In Java](https://nisha-jha.medium.com/collection-framework-in-java-2e0cd92646a2)
- [Collection Framework in Java – Hierarchy, Need & Advantages](https://data-flair.training/blogs/collection-framework-in-java/)

