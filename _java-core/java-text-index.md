---
title: "Text"
sequence: "java-text"
---

## Content


<table>
<tr>
    <th>UTF8</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/text/utf8/'" |
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
    </td>
</tr>
<tr>
    <th>Format</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/text/format/'" |
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
    </td>
</tr>
<tr>
    <th>合并</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/text/concat/'" |
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
    </td>
</tr>
<tr>
    <th>拆分</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/text/split/'" |
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
    </td>
</tr>

<tr>
    <th>排序</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/text/sort/'" |
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
    </td>
</tr>
<tr>
    <th>移除</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/text/remove/'" |
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
    </td>
</tr>
</table>

## Reference

- [lsieun/learn-java-text](https://github.com/lsieun/learn-java-text)
