---
title: "Java ASM 系列一：Core API"
categories: java asm
image: /assets/images/java/asm/brew-your-own-bytecode-with-asm.jpg
tags: java asm
---

[上级目录]({% link _posts/2021-06-01-java-asm.md %})

对于《Java ASM 系列一：Core API》有配套的视频讲解，可以从[这里](https://edu.51cto.com/course/28517.html) 和[这里](https://space.bilibili.com/1321054247/channel/seriesdetail?sid=381716&ctype=0) 进行查看；同时，也可以从[Gitee](https://gitee.com/lsieun/learn-java-asm) 或[Github](https://github.com/lsieun/learn-java-asm) 下载源代码。

---

## 主要内容

### 第一章 基础

{%
assign filtered_posts = site.java-asm-01 |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    {% if num > 100 and num < 200 %}
    <li>
        <a href="{{ post.url }}" target="_blank">{{ post.title }}</a>
    </li>
    {% endif %}
    {% endfor %}
</ol>

### 第二章 生成新的类

{%
assign filtered_posts = site.java-asm-01 |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    {% if num > 200 and num < 300 %}
    <li>
        <a href="{{ post.url }}" target="_blank">{{ post.title }}</a>
    </li>
    {% endif %}
    {% endfor %}
</ol>

### 第三章 转换已有的类

{%
assign filtered_posts = site.java-asm-01 |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    {% if num > 300 and num < 400 %}
    <li>
        <a href="{{ post.url }}" target="_blank">{{ post.title }}</a>
    </li>
    {% endif %}
    
    {% endfor %}
</ol>

### 第四章 工具类和常用类

{%
assign filtered_posts = site.java-asm-01 |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    {% if num > 400 and num < 500 %}
    <li>
        <a href="{{ post.url }}" target="_blank">{{ post.title }}</a>
    </li>
    {% endif %}
    
    {% endfor %}
</ol>


## 参考资料

- 课程源码：[learn-java-asm](https://gitee.com/lsieun/learn-java-asm)
- [ASM 官网](https://asm.ow2.io/)
- ASM 源码：[GitLab](https://gitlab.ow2.org/asm/asm)
- ASM API 文档：[javadoc](https://asm.ow2.io/javadoc/index.html)
- ASM 使用手册：[英文版](https://asm.ow2.io/asm4-guide.pdf)、[中文版](https://www.yuque.com/mikaelzero/asm)
- [ASM mailing list](https://mail.ow2.org/wws/info/asm)
- 参考文献
    - 2002 年，[ASM: a code manipulation tool to implement adaptable systems(PDF)](/assets/pdf/asm-eng.pdf)
    - 2007 年，[Using the ASM framework to implement common Java bytecode transformation patterns(PDF)](/assets/pdf/asm-transformations.pdf)
- [Oracle: The Java Virtual Machine Specification, Java SE 8 Edition](https://docs.oracle.com/javase/specs/jvms/se8/html/index.html)
  - [Chapter 2. The Structure of the Java Virtual Machine](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html)
  - [Chapter 4. The class File Format](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html)
  - [Chapter 6. The Java Virtual Machine Instruction Set](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-6.html)

{:refdef: style="text-align: center;"}
![学习字节码技术 - lsieun.github.io](/assets/images/java/bytecode-lsieun.png)
{:refdef}

{:refdef: style="text-align: center;"}
![QQ Group](/assets/images/contact/qq-group.jpg)
{:refdef}
