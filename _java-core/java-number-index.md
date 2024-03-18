---
title: "Java Number"
sequence: "java-number"
---

Java Number: ASCII, bit, byte, short, char, int, float, long, double, BigInteger.

## Basic

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/number/basic/'" |
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

## Bit~Big

<table>
<tbody>
<tr>
    <th>bit</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/number/bit/'" |
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
    <th>byte</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/number/byte/'" |
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
    <th>int</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/number/int/'" |
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
    <th>float/double</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/number/float/'" |
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
    <th>big</th>
    <td>
{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/number/big/'" |
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
</tbody>
</table>

## Format

{%
assign filtered_posts = site.java-core |
where_exp: "item", "item.url contains '/java-core/number/format/'" |
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

- [lsieun/learn-java-number](https://github.com/lsieun/learn-java-number)

