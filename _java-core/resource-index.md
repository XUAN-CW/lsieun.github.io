---
title: "Resource"
sequence: "java-resource"
---



{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/resources/'" |
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
