---
title: "Git"
image: /assets/images/git/git-vs-github.png
permalink: /git.html
---


Git is software for tracking changes in any set of files,
usually used for coordinating work among programmers collaboratively developing source code during software development.

Git is fundamentally a content-addressable filesystem with a VCS user interface written on top of it.

| User Name   | Email                | Role      |
|-------------|----------------------|-----------|
| Jerry Mouse | jerry@example.com    | Author    |
| Tom Cat     | tom@example.com      | Committer |
| Zhang San   | zhangsan@example.com | Author    |
| Li Si       | lisi@example.com     | Committer |

```text
命令：porcelain plumbing
--------
配置：~/.gitconfig, .git/config
--------
文件格式：git object, index
```

```text
git reset --soft HEAD^
```

## 日常任务

<table>
    <thead>
    <tr>
        <th>Config</th>
        <th>Commit</th>
        <th>Branch</th>
        <th>Repo</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/daily/config/'" |
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
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/daily/commit/'" |
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
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/daily/branch/'" |
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
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/daily/repo/'" |
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

## Overview

{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/overview/'" |
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

## Command

### Workdir + Index + Commit

<table>
    <thead>
    <tr>
        <th>Working Directory</th>
        <th>Index</th>
        <th>Commit</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/cmd/workdir/'" |
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
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/cmd/index/'" |
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
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/cmd/commit/'" |
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

### Branch + Repo

<table>
    <thead>
    <tr>
        <th>Branch</th>
        <th>Repository</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/cmd/branch/'" |
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
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/cmd/repo/'" |
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

### VS

<table>
    <thead>
    <tr>
        <th>VS</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/cmd/vs/'" |
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


## Configuration

{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/config/'" |
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

## Github

{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/github/'" |
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

## Host

{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/host/'" |
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

## plumbing

{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/plumbing/'" |
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

## Git Internals

Git Objects [lsieun/lsieun-git][lsieun-git]

{%
assign filtered_posts = site.git |
where_exp: "item", "item.url contains '/git/git-objects/'" |
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



## References

Doc

- [Reference](https://git-scm.com/docs): 各种命令

Ebook: 电子书

- [Ebook: Pro Git book](http://git-scm.com/book/en/v2)
- [The Git Community Book](https://shafiul.github.io//gitbook/index.html)
- Git In Practice
- Version Control with Git, 2nd Edition

Blog: 关于某一主题的系列文章，可能是不连贯的

- [AlBlue's Blog](https://alblue.bandlem.com/Tag/git/)
- [Reimplementing "git clone" in Haskell from the bottom up](https://stefan.saasen.me/articles/git-clone-in-haskell-from-the-bottom-up/)

Tutorial: 连贯且系统的教程

- [Git 大全](https://gitee.com/all-about-git)
- [Git Magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/pr01.html)
- [30 天精通 Git 版本控管](https://github.com/doggy8088/Learn-Git-in-30-days)
- [Github: cirosantilli/git-tutorial](https://github.com/cirosantilli/git-tutorial)

Tools

- [GitHub Desktop](https://desktop.github.com/)

- [Shields IO](https://shields.io/)

[lsieun-git]: https://github.com/lsieun/lsieun-git
