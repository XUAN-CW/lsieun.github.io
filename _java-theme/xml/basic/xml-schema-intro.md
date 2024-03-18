---
title: "XML Schema"
sequence: "111"
---

What is a schema?

The word schema means a diagram, plan, or framework.
In XML, it refers to a document that describes an XML document.

An XML Schema describes the structure of an XML document.

The XML Schema language is also referred to as **XML Schema Definition** (**XSD**).


XML Schema也是一种用于定义和描述XML文档结构与内容的模式语言，其出现是为了克服DTD的局限性。

XML Schema出现的时间，应该比DTD要晚：查一下时间线。

XML Schema对**名称空间**支持得非常好

名称空间：告诉XML文档的元素被哪个schema文档约束

The XML Schema 1.0 definition language specifies **the structure of an XML document** and **constrains its content**.
The key concept to understand is that a schema based on the XML Schema language defines a class of **valid** XML documents.
A document is considered **valid** with respect to a schema if it conforms to the structure defined by the schema.

A **valid** XML document is formally referred to as an **instance** of the schema document.
As a rough analogy, what a Java class is to a Java object, a schema is to an XML document.

One more important point to keep in mind is that **a schema is also an XML document**.
In fact, this was one of the key motivations for the XML Schema language;
the alternative structure standard, which is a **DTD**, is not an XML document.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<catalog>
    <journal data="2004-05-05">
        <article>
            <title>Java and XML</title>
            <author>Liu Sen</author>
        </article>
    </journal>
</catalog>
```

A schema can be used to validate:

- The structure of elements and attributes.
- The order of elements.
- The data values of elements and attributes, based on ranges, enumerations, and pattern matching.
- The uniqueness of values in an instance.
- A schema can insert **default** and **fixed values** for elements and attributes and normalize **whitespace** according to the type.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema xmlns="https://lsieun.github.io/assets/xml/company"
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"
            targetNamespace="https://lsieun.github.io/assets/xml/company"
            elementFormDefault="qualified">

    <xsd:element name="company" type="companyType"/>
    <xsd:complexType name="companyType">
        <xsd:sequence>
            <xsd:element name="website" type="xsd:string" minOccurs="1"/>
            <xsd:element ref="department" minOccurs="1"/>
        </xsd:sequence>
        <xsd:attribute name="since" type="xsd:date"/>
    </xsd:complexType>

    <xsd:element name="department" type="departmentType"/>
    <xsd:complexType name="departmentType">
        <xsd:sequence>
            <xsd:element ref="employee" minOccurs="0" maxOccurs="unbounded"/>
        </xsd:sequence>
    </xsd:complexType>

    <xsd:element name="employee" type="employeeType"/>
    <xsd:complexType name="employeeType">
        <xsd:sequence>
            <xsd:element name="first-name" type="xsd:string"/>
            <xsd:element name="last-name" type="xsd:string"/>
            <xsd:element name="age" type="ageType"/>
        </xsd:sequence>
    </xsd:complexType>

    <xsd:simpleType name="ageType">
        <xsd:restriction base="xsd:integer">
            <xsd:minInclusive value="1"/>
            <xsd:maxInclusive value="100"/>
        </xsd:restriction>
    </xsd:simpleType>
</xsd:schema>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<company xmlns="https://lsieun.github.io/assets/xml/company"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://lsieun.github.io/assets/xml/company ../xsd/company.xsd"
         since="2022-01-01">

    <website>https://lsieun.github.io</website>

    <department>
        <employee>
            <first-name>Tom</first-name>
            <last-name>Cat</last-name>
            <age>10</age>
        </employee>
    </department>
</company>
```

## The components of XML Schema

Schemas are made up of a number of components of different kinds.

| Component           | Can be named? | Can be unnamed? | Can be global? | Can be local? |
|---------------------|---------------|-----------------|----------------|---------------|
| Element             | yes           | no              | yes            | yes           |
| Attribute           | yes           | no              | yes            | yes           |
| Simple type         | yes           | yes             | yes            | yes           |
| Complex type        | yes           | yes             | yes            | yes           |
| Notation            | yes           | no              | yes            | no            |
| Named model group   | yes           | no              | yes            | no            |
| Attribute group     | yes           | no              | yes            | no            |
| Identity constraint | yes           | no              | no             | yes           |



### Declarations vs. Definitions

Schemas contain both **declarations** and **definitions**.

The term **declaration** is used for components that can appear in the instance and be validated by name.
This includes elements, attributes, and notations.

The term **definition** is used for other components that are **internal to the schema**,
such as complex and simple types, model groups, attribute groups, and identity constraints.

The order of declarations and definitions in the schema document is insignificant.
A declaration can refer to other declarations or definitions that appear before or after it,
or even those that appear in another schema document.

### Global vs. local components

Components can be declared (or defined) **globally** or **locally**.

**Global components** appear at the top level of a schema document, and they are always named.
Their names must be unique, within their component type, within the entire schema.
For example, it is not legal to have two global element declarations with the same name in the same schema.
However, it is legal to have an element declaration and a complex type definition with the same name.

**Local components**, on the other hand, are scoped to the definition or declaration that contains them.
Element and attribute declarations can be local,
which means their scope is the complex type in which they are declared.
Simple types and complex types can also be locally defined,
in which case they are anonymous and cannot be used by any element
or attribute declaration other than the one in which they are defined.

## Elements and attributes

**Elements** and **attributes** are the basic building blocks of XML documents.

### The tag/type distinction

Each of the **elements** and **attributes** is associated with a `type`.

XML Schema separates the concepts of elements and attributes from their types.

## Types

**Types** allow for validation of the **content of elements** and the **values of attributes**.
They can be either **simple types** or **complex types**.

### Simple vs. complex types

**Elements** that have been assigned **simple types** have **character data content**, but no **child elements** or **attributes**.

By contrast, **elements** that have been assigned **complex types** may have **child elements** or **attributes**.

**Attributes** always have **simple types**, not complex types.
This makes sense, because attributes themselves cannot have children or other attributes.

### Named vs. anonymous types

Types can be either **named** or **anonymous**.

**Named types** are always defined globally (at the top level of a schema document)
and are required to have **a unique name**.

**Anonymous types**, on the other hand, must not have names.
They are always defined entirely within an **element** or **attribute declaration**,
and may only be used once, by that declaration.

### The type definition hierarchy

XML Schema allows types to be **derived** from other types.

A complex type can also be derived from another type, either **simple** or **complex**.
It can either **restrict** or **extend** the other type.

The derivation of types from other types forms a **type definition hierarchy**.
Derived types are related to their ancestors and inherit qualities from them.

## Simple types

### Built-in simple types

Forty-nine simple types are built into the XML Schema recommendation.
These simple types represent common data types such as strings, numbers, date and time values,
and also include types for each of the valid attribute types in XML DTDs.

```text
                                                              ┌─── string
                                                              │
                                                              ├─── normalizedString
                                                              │
                                                              ├─── token
                                                              │
                                    ┌─── Strings and names ───┼─── Name
                                    │                         │
                                    │                         ├─── NCName
                                    │                         │
                                    │                         ├─── QName
                                    │                         │
                                    │                         └─── language
                                    │
                                    │                         ┌─── float
                                    │                         │
                                    │                         ├─── double
                                    │                         │
                                    │                         ├─── decimal
                                    │                         │
                                    │                         ├─── integer
                                    │                         │
                                    │                         ├─── long
                                    │                         │
                                    │                         ├─── int
                                    │                         │
                                    │                         ├─── short
                                    │                         │
                                    │                         ├─── byte
                                    ├─── Numeric ─────────────┤
                                    │                         ├─── positiveInteger
                                    │                         │
                                    │                         ├─── nonPositiveInteger
                                    │                         │
                                    │                         ├─── negativeInteger
                                    │                         │
                                    │                         ├─── nonNegativeInteger
                                    │                         │
                                    │                         ├─── unsignedLong
                                    │                         │
                                    │                         ├─── unsignedInt
                                    │                         │
                                    │                         ├─── unsignedShort
                                    │                         │
                                    │                         └─── unsignedByte
                                    │
                                    │                         ┌─── duration
                                    │                         │
XML Schema Built-in simple types ───┤                         ├─── dateTime
                                    │                         │
                                    │                         ├─── date
                                    │                         │
                                    │                         ├─── time
                                    │                         │
                                    │                         ├─── gYear
                                    │                         │
                                    │                         ├─── gYearMonth
                                    ├─── Date and time ───────┤
                                    │                         ├─── gMonth
                                    │                         │
                                    │                         ├─── gMonthDay
                                    │                         │
                                    │                         ├─── gDay
                                    │                         │
                                    │                         ├─── dayTimeDuration (1.1)
                                    │                         │
                                    │                         ├─── yearMonthDuration (1.1)
                                    │                         │
                                    │                         └─── dateTimeStamp (1.1)
                                    │
                                    │                         ┌─── ID
                                    │                         │
                                    │                         ├─── IDREF
                                    │                         │
                                    │                         ├─── IDREFS
                                    │                         │
                                    │                         ├─── ENTITY
                                    ├─── XML DTD types ───────┤
                                    │                         ├─── ENTITIES
                                    │                         │
                                    │                         ├─── NMTOKEN
                                    │                         │
                                    │                         ├─── NMTOKENS
                                    │                         │
                                    │                         └─── NOTATION
                                    │
                                    │
                                    │                         ┌─── boolean
                                    │                         │
                                    │                         ├─── hexBinary
                                    └─── Other ───────────────┤
                                                              ├─── base64Binary
                                                              │
                                                              └─── anyURI
```

### Restricting simple types

New simple types may be derived from other simple types by restricting them.

Using the fourteen facets that are part of XML Schema,
you can specify a valid range of values, constrain the length and precision of values,
enumerate a list of valid values, or specify a regular expression that valid values must match.

```text
                                                          ┌─── minInclusive
                                                          │
                                                          ├─── maxInclusive
                     ┌─── Bounds ─────────────────────────┤
                     │                                    ├─── minExclusive
                     │                                    │
                     │                                    └─── maxExclusive
                     │
                     │                                    ┌─── length
                     │                                    │
                     ├─── Length ─────────────────────────┼─── minLength
                     │                                    │
                     │                                    └─── maxLength
                     │
                     │                                    ┌─── totalDigits
XML Schema Facets ───┼─── Precision ──────────────────────┤
                     │                                    └─── fractionDigits
                     │
                     ├─── Enumerated values ──────────────┼─── enumeration
                     │
                     ├─── Pattern matching ───────────────┼─── pattern
                     │
                     ├─── Whitespace processing ──────────┼─── whiteSpace
                     │
                     ├─── XPath-based assertions (1.1) ───┼─── assertion
                     │
                     │
                     └─── Time zone requirements (1.1) ───┼─── explicitTimezone
```

### List and union types

Most simple types, including those we have seen so far, are **atomic types**.
They contain values that are indivisible.
There are two other varieties of simple types: **list** and **union types**.

**List types** have values that are whitespace-separated lists of **atomic values**.

**Union types** may have values that are either **atomic values** or **list values**.

## Complex types

{:refdef: style="text-align: center;"}
![](/assets/images/xml/xml-schema-element-content-type-and-model.png)
{:refdef}

### Content types

The "content" of an element is the **character data** and **child elements** that are between its tags.

There are four types of content for complex types: **simple**, **element-only**, **mixed**, and **empty**.

The **content type** is independent of **attributes**; all of these **content types** allow **attributes**.

### Content models

The **order** and **structure** of the **child elements** of a **complex type** are known as its **content model**.

**Content models** are defined using a combination of **model groups**, **element declarations or references**, and **wildcards**.

There are three kinds of **model groups**:

- `sequence` groups require that the child elements appear in the order specified.
- `choice` groups allow any one of several child elements to appear.
- `all` groups allow child elements to appear in any order.

这里讲的是“集合”与“单个元素”之间的关系。简单总结：

- `sequence`代表“有序”
- `all`代表“无序”
- `choice`代表“多选一”

These groups can be nested and may occur multiple times, allowing you to create sophisticated content models.

An `any` element is known as a **wildcard**, and it allows for open content models.
There is an equivalent wildcard for attributes, `anyAttribute`, which allows any attribute to appear in a complex type.

### Deriving complex types

**Complex types** may be derived from other types either by **restriction** or by **extension**.

**Restriction**, as the name suggests, restricts the valid contents of a type.
The values for the new type are a subset of those for the base type.
All values of the restricted type are also valid according to the base type.

**Extension** allows for adding additional **child elements** and/or **attributes** to a type,
thus extending the contents of the type.
Values of the base type are not necessarily valid for the extended type,
since required elements or attributes may be added.
New element declarations or references may only be added to the end of a content model.

## Schema composition

An XSD schema is a set of components such as **type definitions** and **element declarations**.

However, a schema could also be represented by an assembly of schema documents.

One way to compose them is through the `include` and `import` mechanisms.

- **Include** is used when the other schema document has the same target namespace as the "main" schema document.
- **Import** is used when the other schema document has a different target namespace.

The `include` and `import` mechanisms are not the only way for processors to assemble schema documents into a schema.
Unfortunately, there is not always a "main" schema document that represents the whole schema.
Instead, a processor might join schema documents from various predefined locations, or take multiple hints from the instance.

## Instances and schemas

A document that conforms to a **schema** is known as an **instance**.
An instance can be validated against a particular schema,
which may be made up of the schema components defined in multiple schema documents.

A number of different ways exist for the **schema** documents to be located for a particular **instance**.
One way is using the `xsi:schemaLocation` attribute. 

Using `xsi:schemaLocation` is not the only way to tell the processor where to find the schema.
XML Schema is deliberately flexible on this topic,
allowing processors to use different methods for choosing schema documents to validate a particular instance.
These methods include **built-in schemas**, use of **internal catalogs**,
use of the `xsi:schemaLocation` attribute, and **dereferencing of namespaces**.

## Annotations

XML Schema provides many mechanisms for describing the structure of XML documents.
However, it cannot express everything there is to know about an instance or the data it contains.

For this reason, XML Schema allows **annotations** to be added to almost any schema component.
These annotations can contain human-readable information
(under `documentation`) or application information (under `appinfo`).

## Advanced features

### Named groups

XML Schema provides the ability to define **groups of element and attribute declarations**
that are reusable by many complex types.
This facility promotes reuse of schema components and eases maintenance.
**Named model groups** are fragments of content models,
and **attribute groups** are bundles of related attributes that are commonly used together.

### Identity constraints

Identity constraints allow you to uniquely identify nodes in a document and
ensure the integrity of references between them.
They are similar to the primary and foreign keys in databases.

### Substitution groups

**Substitution groups** are a flexible way to designate **certain element declarations** as
substitutes for **other element declarations** in content models.
If you have a group of related elements that may appear interchangeably in instances,
you can reference the substitution group as a whole in content models.
You can easily add new element declarations to the substitution groups,
from other schema documents, and even other namespaces,
without changing the original declarations in any way.

### Redefinition and overriding

**Redefinition** and **overriding** allow you to define a new version of a schema component while keeping the same name.
This is useful for extending or creating a subset of an existing schema document,
or overriding the definitions of components in a schema document.

### Assertions

Assertions are XPath constraints on XML data,
which allow complex validation above and beyond what can be specified in a content model.
This is especially useful for co-constraints,
where the values or existence of certain child elements or
attributes affect the validity of other child elements or attributes.
