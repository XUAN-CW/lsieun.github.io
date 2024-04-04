---
title: "Design Patterns"
image: /assets/images/design-pattern/design-pattern-cover.png
permalink: /design-pattern.html
---

In software engineering, a design pattern is a general repeatable solution
to a commonly occurring problem in software design.

编程思路

- 面向对象
- 设计原则
- 设计模式
- 设计应用

## Basic

<table>
    <thead>
    <tr>
        <th>Basic</th>
        <th>Principle</th>
        <th>Creation</th>
        <th>Structure</th>
        <th>Behavior</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.design-pattern |
where_exp: "item", "item.url contains '/design-pattern/basic/'" |
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
assign filtered_posts = site.design-pattern |
where_exp: "item", "item.url contains '/design-pattern/principle/'" |
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
assign filtered_posts = site.design-pattern |
where_exp: "item", "item.url contains '/design-pattern/creation/'" |
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
assign filtered_posts = site.design-pattern |
where_exp: "item", "item.url contains '/design-pattern/structure/'" |
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
assign filtered_posts = site.design-pattern |
where_exp: "item", "item.url contains '/design-pattern/behavior/'" |
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

## References

- [lsieun/learn-java-design-pattern](https://github.com/lsieun/learn-java-design-pattern)

- [Wiki: SOLID](https://en.wikipedia.org/wiki/SOLID)
- Wiki: GRASP: `https://en.wikipedia.org/wiki/GRASP_(object-oriented_design)`

Baeldung:

- [Baeldung Tag: Design Patterns](https://www.baeldung.com/cs/tag/design-patterns)

相关书籍

- Head First Design Patterns
- Design Patterns: Elements of Reusable Object-Oriented Software

视频：

- [编程思想介绍](https://www.bilibili.com/video/BV1Xv4y1T7by/)
- [华为大佬 11 小时讲完的设计模式](https://www.bilibili.com/video/BV17W4y1X74R)

系列文章

- [refactoring.guru: DESIGN PATTERNS](https://refactoring.guru/design-patterns)
- [sourcecodeexamples: Design Patterns Overview](https://www.sourcecodeexamples.net/2017/12/design-patterns-overview.html)
    - [Github:sourcecodeexamples 源码](https://github.com/RameshMF/gof-java-design-patterns)
- [The Software Architecture Chronicles](https://herbertograca.com/2017/07/03/the-software-architecture-chronicles/)
- [Design Patterns in Java Tutorial](https://www.tutorialspoint.com/design_pattern/index.htm)

单独文章

Bilibili

- [深入解读 23 种设计模式](https://www.bilibili.com/video/BV1fR4y1N74H)

- [设计模式之美](https://github.com/jianglinyang8/beauty-of-design-pattern)
