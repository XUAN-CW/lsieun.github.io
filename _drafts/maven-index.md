---
title: "Apache Maven"
image: /assets/images/apache-maven/apache-maven-cover.png
permalink: /maven.html
---

Maven is a build automation tool used primarily for Java projects.

- Maven 软件的配置
  - Repository
- Project 层面的配置

## Content

### 第一章 软件层面

### Maven

<table>
    <thead>
    <tr>
        <th>Basic</th>
        <th>Properties</th>
        <th>LifeCycle</th>
        <th>Repository</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/basic/'" |
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
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/properties/'" |
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
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/lifecycle/'" |
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
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/repository/'" |
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

### JVM

{%
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/jvm/'" |
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

## 项目层面

### Jar 包依赖

<table>
    <thead>
    <tr>
        <th>Dependency</th>
        <th></th>
        <th></th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/dependency/'" |
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
        <td></td>
        <td></td>
    </tr>
    </tbody>
</table>

### 插件

<table>
    <thead>
    <tr>
        <th>插件</th>
        <th>插件配置</th>
        <th>插件管理</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/plugins/'" |
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
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/plugin-configuration/'" |
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
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/plugin-manage/'" |
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

### 多模块

## Deploy

{%
assign filtered_posts = site.apache-maven |
where_exp: "item", "item.url contains '/apache-maven/deploy/'" |
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

```xml
<properties>
    <!-- Resource -->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>

    <!-- JDK -->
    <java.version>8</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
</properties>
```

```text
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <java.version>1.8</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
</properties>

<build>
    <plugins>
        <!-- Java Compiler -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>${java.version}</source>
                <target>${java.version}</target>
                <fork>true</fork>
                <compilerArgs>
                    <arg>-g</arg>
                    <arg>-parameters</arg>
                    <arg>-XDignore.symbol.file</arg>
                </compilerArgs>
            </configuration>
        </plugin>
    </plugins>
</build>
```

### 第三章 高级应用

- [插件开发]({% link _apache-maven/maven-plugin-dev.md %})

## References

- [Apache Maven](https://maven.apache.org/)

Ebook

- 《Apache Maven Cookbook》，作者 Raghuram Bharathan

- [MVN Repository](https://mvnrepository.com/)
- [sonatype/Maven Central Repository Search](https://central.sonatype.com/) [New](https://central.sonatype.dev/)

Baeldung

- [Maven](https://www.baeldung.com/category/maven/)

CSDN

- [Maven](https://blog.csdn.net/liupeifeng3514/category_7500193.html)
- [Maven学习与理解(彻底理解Maven)](https://blog.csdn.net/dghkgjlh/article/details/113471655)

