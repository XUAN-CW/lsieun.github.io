---
title: "UML"
image: /assets/images/uml/plantuml/plantuml-intro-feature.png
permalink: /uml.html
---

**UML**, short for **Unified Modeling Language**,
is a standardized modeling language consisting of an integrated set of diagrams,
developed to help system and software developers for specifying, visualizing, constructing,
and documenting the artifacts of software systems,
as well as for business modeling and other non-software systems.

## Basic

<table>
    <thead>
    <tr>
        <th>Basic</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.uml |
where_exp: "item", "item.url contains '/uml/basic/'" |
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

## PlantUML

<table>
    <thead>
    <tr>
        <th>Class Diagram</th>
        <th>Object Diagram</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.uml |
where_exp: "item", "item.url contains '/uml/plantuml/class/'" |
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
assign filtered_posts = site.uml |
where_exp: "item", "item.url contains '/uml/plantuml/object/'" |
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

- [PlantUML](https://plantuml.com/)
    - [Guide](https://plantuml.com/guide)
    - [Class Diagram](https://plantuml.com/class-diagram)
    - [Preprocessing](https://plantuml.com/preprocessing)
    - [在线测试](https://www.plantuml.com/plantuml/uml/)

- [GitHub: plantuml/plantuml.js](https://github.com/plantuml/plantuml.js)

- [What is Unified Modeling Language (UML)?](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-uml/)
- [PlantUML tutorial to create diagrams as code](https://www.augmentedmind.de/2021/01/03/plantuml-tutorial-diagrams-as-code/)
- [Relationships in class diagrams](https://www.ibm.com/docs/en/rational-soft-arch/9.7.0?topic=diagrams-relationships-in-class)

- [UML Tutorial](https://www.javatpoint.com/uml)
