---
title: "XML Namespaces"
sequence: "111"
---

Namespaces are defined by a separate W3C recommendation called **Namespaces in XML**,
which is in two versions: [1.0](https://www.w3.org/TR/xml-names/) and [1.1](https://www.w3.org/TR/xml-names11/).



An XML Namespace associates **an element or attribute name** with **a specified URI** and
thus allows for multiple elements (or attributes) within an XML document to have the same name
yet have different semantics associated with those names
because they belong to different XML Namespaces.

The key point to understand is that the sole purpose of associating **a uniform resource indicator (URI)** to a **namespace**
is to associate **a unique value** with a namespace.

**There is absolutely no requirement that the URI should point to anything meaningful.**

## Namespace names

Namespace names are Uniform Resource Identifiers (URIs).
URIs encompass URLs of various schemes (e.g., HTTP, FTP, gopher, telnet), as well as URNs (Uniform Resource Names).
Many namespaces are written in the form of HTTP URLs.

The main purpose of a namespace is not to point to a location where a resource resides.
Instead, much like a Java package name, it is intended to provide a unique name that can be associated with a particular person or organization.
Therefore, namespace names are not required to be dereferenceable.

The namespace URI could point to a schema, an HTML page, a directory of resources, or nothing at all.



## Namespace declarations and prefixes

An instance may include one or more namespace declarations that relate **elements** and **attributes** to namespaces.
This happens through a `prefix`, which serves as a proxy for the namespace.

A namespace is declared using a special attribute whose name starts with the letters `xmlns`.

Although the instance author may choose prefixes arbitrarily,
there are commonly used prefixes for some namespaces.

- `xsl`: **Extensible Stylesheet Language** (XSL) namespace
- `xsd` or `xs`: XML Schema Namespace

```text
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"/>
```

```text
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
```

For the , the commonly used prefixes are .

## Namespace Definition

You specify an XML Namespace through one of two reserved attributes:

- You can specify a default XML Namespace URI using the `xmlns` attribute.
- You can specify a nondefault XML Namespace URI using the `xmlns:prefix` attribute,
  where `prefix` is a unique prefix associated with this XML Namespace.

## Name terminology

In the context of namespaces, there are several different kinds of names.

**Qualified names**, known as **QNames**, are names that are qualified with a namespace name.
This may happen one of two ways:

- The name contains a prefix that is mapped to a namespace.
- The name does not contain a prefix, but there is a default namespace declared for that element.
  This applies only to **elements**; there is no such thing as an unprefixed, qualified **attribute** name.

**Unqualified names**, on the other hand, are names that are not in any namespace.

- For **element names**, this means they are unprefixed and there is no default namespace declaration.
- For **attribute names**, this means they are unprefixed, period.

**Prefixed names** are names that contain a namespace prefix, such as `prod:product`.
Prefixed names are qualified names, assuming there is a namespace declaration for that prefix in scope.

**Unprefixed names** are names that do not contain a prefix, such as `items`.
Unprefixed element names can be either qualified or unqualified, depending on whether there is a default namespace declaration.

A **local name** is the part of a qualified name that is not the prefix.

**Non-colonized names**, known as **NCNames**, are simply XML names that do not contain colons.
All **local names** and **unprefixed names** are NCNames. Prefixes are also NCNames, because they follow these same rules.

## Scope of namespace declarations

The scope of a namespace declaration is the element in whose start tag it appears,
and all of its children, grandchildren, and so on.

Generally, it is preferable to put all your namespace declarations in the root element's start tag.
It allows you to see at a glance what namespaces a document uses,
there is no confusion about their scopes, and it keeps them from cluttering the rest of the document.

## Overriding namespace declarations

Namespace declarations can also be overridden.
If a namespace declaration appears within the scope of another namespace declaration with the same prefix, it overrides it.

Likewise, if a default namespace declaration appears within the scope of another default namespace declaration,
it overrides it.

## Undeclaring namespaces

A default namespace declaration may also be the empty string (that is, `xmlns=""`).
This means that unprefixed element names in its scope are not in any namespace.
This can be used to essentially "undeclare" the default namespace.

In version 1.1 (but not in 1.0), you can also undeclare a prefix by using an empty string.

## Attributes and namespaces

The relationship between attributes and namespaces is slightly simpler than the relationship between elements and namespaces.
Prefixed attribute names, as you would expect, are in whichever namespace is mapped to that prefix.
Attributes with prefixed names are sometimes referred to as **global attributes**.
Unprefixed attribute names, however, are never in a namespace.
This is because they are not affected by default namespace declarations.

Some people make the argument that an unprefixed attribute is (or should be) in the namespace of its parent element.
While it may be indirectly associated with that namespace, it is not directly in it.
For the purposes of writing schemas and using other XML technologies such as XSLT and XQuery,
you should treat an unprefixed attribute as if it were in no namespace at all.

## The relationship between namespaces and schemas

**Namespaces** and **schemas** have a many-to-many relationship.

A namespace can have names defined in any number of schemas.
A namespace can exist without any schema.
Some namespaces have one schema that defines its names.
Other namespaces have multiple schemas.
These schemas may be designed to be used together, or be completely incompatible with each other.
They could present different perspectives on the same information,
or be designed for different purposes such as varying levels of validation or system documentation.
They could be different versions of each other.
There are no rules that prevent several schemas from utilizing the same namespace, with overlapping declarations.
As long as the processor does not try to validate an instance against all of them at once, this is completely legal.

A schema can declare names for any number of target namespaces.
Some schemas have no target namespace at all.
Other schemas are represented by composing multiple schema documents, each with its own target namespace.

## Element/Attribute + Namespace



An element or an attribute is designated to be part of an XML Namespace
either by explicitly prefixing its name with an XML Namespace prefix
or by implicitly nesting it within an element that has been associated with a default XML Namespace.

It is important to understand
that a namespace `prefix` is merely a syntactic device to impart brevity to a namespace reference and
that **the real namespace** is always **the associated URI**. 






