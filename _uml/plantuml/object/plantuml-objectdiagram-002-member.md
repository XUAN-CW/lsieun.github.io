---
title: "成员"
sequence: "102"
---

[UP](/uml.html)

## Basic

```plantuml
@startuml

object user
user : name = "Dummy"
user : id = 123
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-01.svg)
{:refdef}

```plantuml
@startuml

object user {
  name = "Dummy"
  id = 123
}

@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-01.svg)
{:refdef}

## Map table

You can define a map table with `map` keyword and `=>` separator.

```plantuml
@startuml
map CapitalCity {
 UK => London
 USA => Washington
 Germany => Berlin
}
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-map-01.svg)
{:refdef}

```plantuml
@startuml
map "Map **Contry => CapitalCity**" as CC {
 UK => London
 USA => Washington
 Germany => Berlin
}
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-map-02.svg)
{:refdef}

```plantuml
@startuml
map "map: Map<Integer, String>" as users {
 1 => Alice
 2 => Bob
 3 => Charlie
}
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-map-03.svg)
{:refdef}

## Link

```plantuml
@startuml
object London

map CapitalCity {
 UK *-> London
 USA => Washington
 Germany => Berlin
}
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-link-01.svg)
{:refdef}

```plantuml
@startuml
object London
object Washington
object Berlin
object NewYork

map CapitalCity {
 UK *-> London
 USA *--> Washington
 Germany *---> Berlin
}

NewYork --> CapitalCity::USA
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-link-02.svg)
{:refdef}

```plantuml
@startuml
package foo {
    object baz
}

package bar {
    map A {
        b *-> foo.baz
        c =>
    }
}

A::c --> foo
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-link-03.svg)
{:refdef}

```plantuml
@startuml
object Foo
map Bar {
  abc=>
  def=>
}
object Baz

Bar::abc --> Baz : Label one
Foo --> Bar::def : Label two
@enduml
```

{:refdef: style="text-align: center;"}
![](/assets/images/uml/plantuml/object/object-diagram-obj-fields-link-04.svg)
{:refdef}
