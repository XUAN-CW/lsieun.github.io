---
title: "SVG"
image: /assets/images/svg/svg-cover.png
permalink: /svg.html
---

SVG: Scalable Vector Graphics

## Content

{%
assign filtered_posts = site.svg |
where_exp: "item", "item.url contains '/svg/basic/'" |
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

- [lsieun/learn-java-svg](https://github.com/lsieun/learn-java-svg)

- [JFreeSVG](https://www.jfree.org/jfreesvg/)
    - [GitHub: jfree/jfreesvg](https://github.com/jfree/jfreesvg)
