---
title: "XML Syntax - Basic"
sequence: "102"
---

## XML Declaration

```text
<?xml version="1.0" encoding="UTF-8"?>
```

A well-formed XML document can begin with an XML declaration,
which is special markup telling an XML parser that the document is XML.

> 作用

An XML declaration can be omitted, but if it appears, it should be the first thing within a document.

> 可以省略，位置：第一个

### version

The `version` attribute specifies the XML version, and it is a **required** attribute.

```text
<?xml version="1.0"?>
```

The initial version of this specification (1.0) was introduced in 1998 and is widely implemented.

> XML 1.0是1998年发布

The W3C, which maintains XML, released version 1.1 in 2004.

> XML 1.1是2004年发布

Unlike XML 1.0, XML 1.1 isn't widely implemented and should be used only by those needing its unique features.

> 版本：流行1.0版本

### encoding

The `encoding` attribute specifies the character set used to encode data in an XML document.

> 作用

**XML supports Unicode**,
which means that XML documents consist entirely of characters taken from the Unicode character set.

> 支持的字符集

One common encoding is `UTF-8`, which is a variable-length encoding of the Unicode character set.

> 常用字符集：UTF-8

```text
<?xml version="1.0" encoding="UTF-8"?>
```

In the absence of the XML declaration or when the XML declaration's `encoding` attribute isn't present,
an XML parser typically looks for a special character sequence at the start of a document
to determine the document's encoding.
This character sequence is known as the **byte-order-mark (BOM)**
and is created by an editor program (such as Microsoft Windows Notepad)
when it saves the document according to `UTF-8` or some other encoding.
For example, the hexadecimal sequence `EF BB BF` signifies `UTF-8` as the encoding.
Similarly, `FE FF` signifies `UTF-16` big endian,
`FF FE` signifies UTF-16 little endian,
`00 00 FE FF` signifies UTF-32 big endian,
and `FF FE 00 00` signifies UTF-32 little endian.

> 如果有BOM，则依据BOM来判断encoding

UTF-8 is assumed when no BOM is present.

> 如果没有BOM，则使用UTF-8作为encoding

### standalone

The `standalone` attribute specifies whether the XML document references external entities.
If no external entities are referenced, specify the `standalone` attribute as `yes`.

```text
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
```

This **optional attribute**, which is only relevant with DTDs,
determines if there are external markup declarations
that affect the information passed from an XML processor (a parser) to the application.

> standalone属性与DTD相关

Its value defaults to `no`, implying that there are, or may be, such declarations.
A `yes` value indicates that there are no such declarations.

> 默认值：no

可选择的值：

- yes
- no


## Elements

### Root Element

A document must have **a single root element**, which is also known as the **document element**.

> 在一个XML文档中，有且仅有一个根元素（Root Element）

```text
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<company></company>
```

### Start and End Tags

The building block of XML is the **element**, as that's what comprises XML documents.

> XML文档中，最基本的成员就是element。

An **element** in an XML document is delimited by a **start tag** and an **end tag**.

> element由start tag和end tag分隔。

A **start tag** within an element is delimited by the `<` and `>` characters and has a tag name.

> 开始标签

An **end tag** is delimited by the `</` and `>` character sequences and also contains a tag name.

> 结束标签

```text
                                                      ┌─── name: <company>
                                    ┌─── start tag ───┤
                  ┌─── tag ─────────┤                 └─── attribute: <company name="ABC">
                  │                 │
                  │                 └─── end tag ─────┼─── </company>
                  │
                  │                 ┌─── name
   XML Element ───┼─── attribute ───┤
                  │                 └─── value
                  │
                  │                 ┌─── empty
                  │                 │
                  └─── content ─────┼─── text content ──────┼─── CDATA
                                    │
                                    └─── nested elements
```

### Tag Name

Names in XML must start with either a letter or the underscore character (`_`).  
The rest of the name consists of letters, digits, the underscore character, the dot (`.`), or a hyphen (`-`).  
Spaces are not allowed in names.

- 开头字符：`a-z`, `A-Z`, `_`
- 后续字符：`a-z`, `A-Z`, `_`, `0-9`, `.`, `-`
- 禁用字符：`space`, `&`

合法：（包含`-`）

```text
<copy-right>
```

合法：（包含`.`），在Maven的配置文件中设置的属性信息

```text
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <java.version>1.8</java.version>
</properties>
```

不合法：(数字开头)

```text
<123>
```

不合法：(包含有空格)

```text
<first name>
```

不合法：(包括`&`符号)

```text
<tom&jerry>
```

#### 区分大小写

在XML文件中，标签名字的区分大小写。Unlike HTML, **names are case sensitive in XML**.

以下是不同的不个元素：

```text
<company>
<COMPANY>
<Company>
```

By convention, XML elements are frequently written in lowercase.

#### 命名习惯

When a name consists of several words, the words are usually separated by a hyphen, as in `first-name`.

```xml
<first-name></first-name>
```

Another popular convention is to capitalize the first letter of each word and
use no separation character as in `FirstName`.

```xml
<FirstName></FirstName>
```

### Nested Elements

An element can contain other nested elements.

```text
<?xml version="1.0" encoding="UTF-8"?>
<company>
    <department>
    </department>
</company>
```

### Text Content

Elements may contain text content.

```text
<?xml version="1.0" encoding="UTF-8"?>
<company>
    <department>
        <employee>Tom Cat</employee>
    </department>
</company>
```

#### CDATA construct

Of course, element text content cannot contain any delimiter character sequences such as `</`.
One way to get around that is to enclose element content within a `CDATA` construct:

```text
<?xml version="1.0" encoding="UTF-8"?>
<company>
    <department>
        <employee>
            <![CDATA[This is some arbitrary text <within> a character data]]>
        </employee>
    </department>
</company>
```


Character Data and Markup [Link](https://www.w3.org/TR/REC-xml/#syntax)

**Text** consists of intermingled **character data** and **markup**.

**Markup** takes the form of start-tags, end-tags, empty-element tags, entity references, character references, comments,
CDATA section delimiters, document type declarations, processing instructions, XML declarations, text declarations,
and any white space that is at the top level of the document entity
(that is, outside the document element and not inside any other markup).

**All text** that is not **markup** constitutes the **character data** of the document.

### Empty Element

An element may of course have no nested elements or content.
Such an element is termed an **empty element**, and it can be written with a special start tag that has no end tag.

```text
<?xml version="1.0" encoding="UTF-8"?>
<company>
    <department>
        <employee/>
    </department>
</company>
```



## Attributes

Elements can have attributes, which are specified in the **start tag**.

An attribute is defined as a name-value pair.

### name-value pair

```text
<?xml version="1.0" encoding="UTF-8"?>
<company>
    <department>
        <employee id="001" name="Tom Cat">
        </employee>
    </department>
</company>
```

添加一个`birthday`属性，其值为`<2022-01-01>`：

```text
<?xml version="1.0" encoding="UTF-8"?>
<company>
    <department>
        <employee id="001" name="Tom Cat" birthday="&lt;2022-01-01&gt;">
        </employee>
    </department>
</company>
```

### quotation

Unlike HTML, XML insists on the **quotation marks**.

```xml
<class-file magic="0xCAFEBABE" version="8"></class-file>
```

The XML processor would reject the following:

```text
<class-file magic=0xCAFEBABE version=8></class-file>
```

The **quotation marks** can be either **single** or **double quotes**.
This is convenient if you need to insert single or double quotation marks in an attribute value.

```text
<class-file magic='0xCAFEBABE' version='8'></class-file>
```

## Elements vs. Attributes

In XML, there are no rules about when to use attributes, and when to use child elements.

### Avoid using attributes

Some of the problems with attributes are:

- attributes cannot contain multiple values (child elements can)
- attributes are not easily expandable (for future changes)
- attributes cannot describe structures (child elements can)
- attributes are more difficult to manipulate by program code
- attribute values are not easy to test against a DTD

If you use attributes as containers for data, you end up with documents that are difficult to read and maintain.
Try to use elements to describe data.
Use attributes only to provide information that is not relevant to the data.

Metadata (data about data) should be stored as attributes, and that data itself should be stored as elements.

## Comments

You can define comments in an XML document within a comment declaration:

```text
<!-- This is a comment -->
```

Comments can appear anywhere outside **markup**,
which consists of start tags, end tags, empty element tags, comments, CDATA sections, escape character references, and entity references.



