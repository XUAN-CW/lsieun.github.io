---
title: "Java Stream"
sequence: "stream"
---

To summarize, the Streams API in Java 8 lets you write code that's

- **Declarative** - More concise and readable
- **Composable** - Greater flexibility
- **Parallelizable** - Better performance

## Content

{% 
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/stream/basic/'" |
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

## Operation

{%
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/stream/operation'" |
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

## Numeric

{%
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/stream/numeric'" |
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

- [lsieun/learn-java-stream](https://github.com/lsieun/learn-java-stream)
