---
title: "IntelliJ IDEA"
image: /assets/images/intellij/intellij-idea.png
permalink: /intellij-idea.html
---

IntelliJ IDEA is an integrated development environment written in Java for developing computer software. It is developed by JetBrains.

安装之后，要做的事情：

- [ ] 禁用插件，因为有些用不到。

在 idea 的安装目录的 `plugins` 文件夹，只剩下 `java` 和 `java-ide-customization` 两个文件夹，也能启动。

## 主要内容

### 窗口

目标：将手放在键盘上，尽量不用鼠标

<table>
    <thead>
    <tr>
        <th>Project</th>
        <th>Editor</th>
        <th>Tool</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/window/project/'" |
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
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/window/editor/'" |
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
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/window/tool/'" |
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

### 文本内容

<table>
    <thead>
    <tr>
        <th>代码</th>
        <th>操作</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/content/code/'" |
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
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/content/text/'" |
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

### 键盘+鼠标

<table>
    <thead>
    <tr>
        <th>键盘</th>
        <th>鼠标</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/io/keyboard/'" |
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
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/io/mouse/'" |
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

### 插件

<table>
    <thead>
    <tr>
        <th>常用插件</th>
        <th>工具插件</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/plugins/common/'" |
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
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/plugins/tool/'" |
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

## 配置和原理

Disabling unused plugins

Shared JDK Indexes

{%
assign filtered_posts = site.intellij-idea |
where_exp: "item", "item.url contains '/intellij-idea/index/'" |
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

### IDE Configuration

### Project Configuration


### Source Code


## 参考资料

- [jetbrains.com: Discover IntelliJ IDEA](https://www.jetbrains.com/help/idea/discover-intellij-idea.html)
- [The IntelliJ IDEA Blog](https://blog.jetbrains.com/idea/)
- [IntelliJ IDEA Guide](https://www.jetbrains.com/idea/guide/)

