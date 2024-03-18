---
title: "Unicode"
image: /assets/images/unicode/unicode-cover.jpg
permalink: /unicode.html
---

Unicode, formally the Unicode Standard, is an information technology standard for the consistent encoding, representation, and handling of text expressed in most of the world's writing systems.

- Unicode 自己支持哪些内容
- 不同 Java 版本支持 Unicode 版本不同
- 不同的操作系统支持哪些内容（哪个版本的 Unicode）


{%
assign filtered_posts = site.unicode |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}" target="_blank">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

## Reference

- [learn-unicode](https://github.com/lsieun/learn-unicode)
- [Unicode Character Table](https://unicode-table.com/en/)
  - [Arrow Symbols](https://unicode-table.com/en/sets/arrow-symbols/)
  - [Box Drawing](https://unicode-table.com/en/blocks/box-drawing/)
  - [Geometric Shapes](https://unicode-table.com/en/blocks/geometric-shapes/)
  - [Mathematical Signs](https://unicode-table.com/en/sets/mathematical-signs/)
  - [Star Symbols](https://unicode-table.com/en/sets/star-symbols/)
