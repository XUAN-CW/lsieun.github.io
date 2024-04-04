---
title: "类成员"
sequence: "102"
---

[UP](/uml.html)

## 成员

```plantuml
@startuml

class Dummy {
  String data
  void methods()
}

@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/class/class-diagram-member-basic.svg)
{:refdef}

## 可见性

| Character | Icon for field                                                 | Icon for method                                                 | Visibility        |
|-----------|----------------------------------------------------------------|-----------------------------------------------------------------|-------------------|
| `-`       | ![](/assets/images/uml/plantuml/img/private-field.png)         | ![](/assets/images/uml/plantuml/img/private-method.png)         | `private`         |
| `#`       | ![](/assets/images/uml/plantuml/img/protected-field.png)       | ![](/assets/images/uml/plantuml/img/protected-method.png)       | `protected`       |
| `~`       | ![](/assets/images/uml/plantuml/img/package-private-field.png) | ![](/assets/images/uml/plantuml/img/package-private-method.png) | `package private` |
| `+`       | ![](/assets/images/uml/plantuml/img/public-field.png)          | ![](/assets/images/uml/plantuml/img/public-method.png)          | `public`          |

```plantuml
@startuml
class Dummy {
 -field1
 #field2
 ~method1()
 +method2()
}
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/class/class-diagram-member-visibility.svg)
{:refdef}

## Abstract and Static

You can define static or abstract methods or fields using the `{static}` or `{abstract}` modifier.

```plantuml
@startuml
class Dummy {
  {static} String id
  {abstract} void methods()
}
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/class/class-diagram-member-modifier.svg)
{:refdef}

## Advanced class body

By default, methods and fields are automatically regrouped by PlantUML.

You can use separators to define your own way of ordering fields and methods.
The following separators are possible:

- `--`
- `..`
- `==`
- `__`

```plantuml
@startuml
class Foo1 {
  You can use
  several lines
  ..
  as you want
  and group
  ==
  things together.
  __
  You can have as many groups
  as you want
  --
  End of class
}

class User {
  .. Simple Getter ..
  + getName()
  + getAddress()
  .. Some setter ..
  + setName()
  __ private data __
  int age
  -- encrypted --
  String password
}
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/class/class-diagram-member-advanced.svg)
{:refdef}

## Hide attributes, methods...

You can parameterize the display of classes using the `hide/show` command.

The basic command is: `hide empty members`. This command will hide attributes or methods if they are empty.

Instead of empty members, you can use:

- `empty fields` or `empty attributes` for empty fields,
- `empty methods` for empty methods,
- `fields` or `attributes` which will hide fields, even if they are described,
- `methods` which will hide methods, even if they are described,
- `members` which will hide fields and methods, even if they are described,
- `circle` for the circled character in front of class name,
- `stereotype` for the stereotype.

You can also provide, just after the `hide` or `show` keyword:

- `class` for all classes,
- `interface` for all interfaces,
- `enum` for all enums,
- `<<foo1>>` for classes which are stereotyped with `foo1`,
- an existing class name.

You can use several `show/hide` commands to define rules and exceptions.

```plantuml
@startuml

class Dummy1 {
  +myMethods()
}

class Dummy2 {
  +hiddenMethod()
}

class Dummy3 <<Serializable>> {
String name
}

hide members
hide <<Serializable>> circle
show Dummy1 methods
show <<Serializable>> fields

@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/class/class-diagram-member-hide.svg)
{:refdef}
