---
title: "Java Enum"
sequence: "java-enum"
---



An **enumerated type** is a type whose legal values consist of a fixed set of constants,
such as the seasons of the year,
the planets in the solar system,
or the suits in a deck of playing cards.

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/enum/'" |
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

## 参考

- 《Effective Java》 3rd
