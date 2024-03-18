---
title: "Hydraulic"
image: /assets/images/hydraulic/water-cycle-diagram.webp
permalink: /hydraulic.html
---

Hydraulic

{:refdef: style="text-align: center;"}
![](/assets/images/hydraulic/laminar-left-transitional-middle-and-turbulent-right-flow-arrows.png)
{:refdef}

## Formula

{%
assign filtered_posts = site.hydraulic |
where_exp: "item", "item.url contains '/hydraulic/formula/'" |
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


