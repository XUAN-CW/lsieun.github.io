---
title: "Java XML"
sequence: "xml"
---

XML 1.0 was made a World Wide Web Consortium (W3C) Recommendation in 1998.
The W3C is dedicated to developing interoperable technologies.

## XML

{%
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/xml/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    {% if num > 100 and num < 140 %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}
    {% endfor %}
</ol>

## DOM

{%
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/xml/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    {% if num > 140 and num < 160 %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}
    {% endfor %}
</ol>

## StAX

{%
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/xml/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    {% if num > 160 and num < 180 %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}
    {% endfor %}
</ol>

## XSLT

{%
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/xml/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    {% if num > 180 and num < 200 %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}
    {% endfor %}
</ol>

## XML Parsing

## XML Validation

## All

{%
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/xml/'" |
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

W3C

- XML
  - [XML 1.0](https://www.w3.org/TR/REC-xml/)
  - [XML 1.1](https://www.w3.org/TR/xml11/)
- XML Namespace
  - [Namespaces in XML 1.0](https://www.w3.org/TR/xml-names/)
  - [Namespaces in XML 1.1](https://www.w3.org/TR/xml-names11/)
- [XML Schema](https://www.w3.org/XML/Schema.html)
  - XML Schema 1.0
    - [Part 0: Primer](https://www.w3.org/TR/xmlschema-0/)
    - [Part 1: Structures](https://www.w3.org/TR/xmlschema-1/)
    - [Part 2: Datatypes](https://www.w3.org/TR/xmlschema-2/)
  - XML Schema 1.1
    - [Part 1: Structures](https://www.w3.org/TR/xmlschema11-1/)
    - [Part 2: Datatypes](https://www.w3.org/TR/xmlschema11-2/)
- [XPATH](https://www.w3.org/TR/xpath/)
- [XSLT](https://www.w3.org/TR/xslt/)
- [Document Object Model (DOM) Level 3 Load and Save Specification](https://www.w3.org/TR/DOM-Level-3-LS/)
- [Document Object Model (DOM) Level 3 Core Specification](https://www.w3.org/TR/DOM-Level-3-Core/)
- [SOAP](https://www.w3.org/TR/soap/)
- [WSDL](https://www.w3.org/TR/wsdl/)

w3schools

- [XML Tutorial](https://www.w3schools.com/xml/)
- [DTD Tutorial](https://www.w3schools.com/xml/xml_dtd_intro.asp)

Oracle

- [Java API for XML Processing](https://docs.oracle.com/javase/8/docs/technotes/guides/xml/jaxp/index.html)
- [Java API for XML Processing (JAXP) Tutorial](https://www.oracle.com/java/technologies/jaxp-introduction.html)
- [Trail: Java API for XML Processing (JAXP)](https://docs.oracle.com/javase/tutorial/jaxp/index.html)

Apache

- [The Apache Xerces Project](https://xerces.apache.org/)
  - [Xerces2 Java XML Parser Readme](https://xerces.apache.org/xerces2-j/)
  - [Xerces2 Java XML Parser Features](https://xerces.apache.org/xerces2-j/features.html)

XML.COM

- [xml.com](https://www.xml.com/)
  - [Norman Walsh](https://www.xml.com/pub/au/44)

Other

- [SAX](http://www.saxproject.org/)
- [JAXP (Java API for XML Processing)](https://roytuts.com/jaxp/)
- [JDOM](http://www.jdom.org/)

一些DTD：

- [DTD for XML Schemas: Part 1: Structures](https://www.w3.org/2001/XMLSchema.dtd)
- [DTD for XML Schemas: Part 2: Datatypes](https://www.w3.org/2001/datatypes.dtd)
- [Extensible HTML version 1.0 Transitional DTD](https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd)

一些XSD：

- [2009-XMLSchema.xsd](https://www.w3.org/2009/XMLSchema/XMLSchema.xsd)
- [2001-XMLSchema.xsd](https://www.w3.org/2001/XMLSchema.xsd)
- [spring-beans.xsd](https://www.springframework.org/schema/beans/spring-beans.xsd)
