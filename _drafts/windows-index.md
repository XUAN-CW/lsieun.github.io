---
title: "Windows"
image: /assets/images/windows/novo-windows-microsoft.jpg
permalink: /windows.html
---

Microsoft Windows

## CMD

{%
assign filtered_posts = site.windows |
where_exp: "item", "item.url contains '/windows/cmd/'" |
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

## Software

{%
assign filtered_posts = site.windows |
where_exp: "item", "item.url contains '/windows/software/'" |
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
