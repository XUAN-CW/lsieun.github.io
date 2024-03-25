---
title: "Netty"
image: /assets/images/netty/netty-cover.png
permalink: /netty.html
---

Netty is a non-blocking I/O client-server framework.

- Netty 核心
- Netty 协议

## Basic

<table>
    <thead>
    <tr>
        <th>Concept</th>
        <th>Example</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/basic/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/example/'" |
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

## Component

<table>
    <thead>
    <tr>
        <th>EventLoop</th>
        <th>Channel</th>
        <th>Future & Promise</th>
        <th>Handler & Pipeline</th>
        <th>ByteBuf</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/eventloop/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/channel/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/future/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/handler/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/bytebuf/'" |
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

## Advanced

<table>
    <thead>
    <tr>
        <th>Data</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/data/'" |
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

## Codec

<table>
    <thead>
    <tr>
        <th>Basic</th>
        <th>Decoder</th>
        <th>Encoder</th>
        <th>Codec</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/codec/basic/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/codec/decoder/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/codec/encoder/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/codec/basic/'" |
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

## Protocol

<table>
    <thead>
    <tr>
        <th>HTTP</th>
        <th>WebSocket</th>
        <th>SSL/TLS</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/http/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/websocket/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/ssl/'" |
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

## Option

<table>
    <thead>
    <tr>
        <th>Server</th>
        <th>Client</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/option/server/'" |
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
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/option/client/'" |
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

## Connection

<table>
    <thead>
    <tr>
        <th>连接</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/connection/'" |
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

## Extra

<table>
    <thead>
    <tr>
        <th>Extra</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/extra/'" |
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

## 源码

<table>
    <thead>
    <tr>
        <th>源码</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/src/'" |
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

- [lsieun/learn-java-netty](https://github.com/lsieun/learn-java-netty)

- [Netty](https://netty.io/)

- [GitHub: netty/netty](https://github.com/netty/netty)
  - [4.1.x 示例](https://github.com/netty/netty/tree/4.1/example/src/main/java/io/netty/example)

- [Baeldung Tag: Netty](https://www.baeldung.com/tag/netty)
    - [Introduction to Netty](https://www.baeldung.com/netty)
    - [HTTP Server with Netty](https://www.baeldung.com/java-netty-http-server)
    - [HTTP/2 in Netty](https://www.baeldung.com/netty-http2)

- [黑马程序员Netty全套教程](https://www.bilibili.com/video/BV1py4y1E7oA/)
    - [文档](https://nyimac.gitee.io/2021/04/25/Netty%E5%9F%BA%E7%A1%80/)

- [GitHub: beardlessCat/im](https://github.com/beardlessCat/im)


