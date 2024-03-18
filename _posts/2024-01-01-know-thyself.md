---
title: "Know Thyself"
image: /assets/images/thyself/know-thyself.png
---

"Know thyself" is a philosophical maxim
which was inscribed upon the Temple of Apollo in the ancient Greek precinct of Delphi.

## Content

{%
assign filtered_posts = site.thyself |
where_exp: "item", "item.url contains '/thyself/'" |
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

- [Know thyself: how self-awareness helps you at work](https://www.atlassian.com/blog/teamwork/know-thyself-how-self-awareness-helps-you-at-work)
- [How to Develop Self-Knowledge and Why it Matters](https://proveritas.com.au/blog-home/how-to-develop-self-knowledge-and-why-it-matters)

