---
title: "Java NIO"
image: /assets/images/java/nio/asynchronous-programming.jpg
permalink: /java-nio.html
---

Java NIO (New IO) is an alternative IO API for Java,
meaning alternative to the standard Java IO and Java Networking API.

## NIO Basic

<table>
    <thead>
    <tr>
        <th>Buffer</th>
        <th>Channel</th>
        <th>Selector</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/nio/basic/buffer/'" |
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
where_exp: "item", "item.url contains '/java/nio/basic/channel/'" |
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
where_exp: "item", "item.url contains '/java/nio/basic/selector/'" |
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

## 文件

{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/nio/file/'" |
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

## 网络

<table>
    <thead>
    <tr>
        <th>Channel</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/nio/network/channel/'" |
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

## Reference

- [lsieun/learn-java-nio](https://github.com/lsieun/learn-java-nio)

- [Oracle: Java NIO](https://docs.oracle.com/en/java/javase/21/core/java-nio.html)
- [Java NIO](https://www.educba.com/java-nio/)
- [Understanding File Operations in Java: Working with Files using java.io and java.nio](https://clouddevs.com/java/file-operations/)
- [Asynchronous programming. Blocking I/O and non-blocking I/O](https://luminousmen.com/post/asynchronous-programming-blocking-and-non-blocking)
- [Java NIO Tutorial](https://jenkov.com/tutorials/java-nio/index.html)
- [Java IO vs NIO](https://www.baeldung.com/java-io-vs-nio)
- [Introduction to Java NIO with Examples](https://www.geeksforgeeks.org/introduction-to-java-nio-with-examples/)

- IPMSG
    - [IP Messenger](https://ipmsg.org/)
    - [mcxiao/ipmsg4j](https://github.com/mcxiao/ipmsg4j)
    - [Afauria/IPMsg](https://github.com/Afauria/IPMsg)
    - [hyberbin/J-Feiq](https://github.com/hyberbin/J-Feiq)
    - [pankajsinghal/ip-messenger](https://github.com/pankajsinghal/ip-messenger)
