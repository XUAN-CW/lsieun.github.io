---
title: "Java IO"
image: /assets/images/java/io/java-io.jpg
permalink: /java-io.html
---

Java IO

## 控制台

<table>
    <thead>
    <tr>
        <th>读数据</th>
        <th>写数据</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/io/console/in/'" |
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
        <td>
{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/io/console/out/'" |
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

{:refdef: style="text-align: center;"}
![](/assets/images/java/io/java-basic-input-output.png)
{:refdef}

## 文件系统

<table>
    <thead>
    <tr>
        <th>Directory</th>
        <th>File</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/io/filesystem/directory/'" |
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
        <td>
{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/io/filesystem/file/'" |
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

## 文件内容

{:refdef: style="text-align: center;"}
![](/assets/images/java/io/types-of-java-io-streams.png)
{:refdef}


## 数据传输



## Reference

- [Baeldung: Java IO](https://www.baeldung.com/tag/java-io)

