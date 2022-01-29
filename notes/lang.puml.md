---
id: 35a22ebd-29ee-4ecf-8068-74347c4578b7
title: Puml
desc: ''
updated: 1641557866037
created: 1605773790054
---

# PlantUML

## Component Diagrams

### Shapes
```puml
@startuml
component "A" as a
node "B" as b
interface "C" as c
@enduml
```

### Styling
Colours for classes
```sh
component "A" as a <<push>>
skinparam component {
  backgroundColor<<push>> #95e683
}
```
```puml
@startuml
component "A" as a <<push>>
skinparam component {
  backgroundColor<<push>> #95e683
}
@enduml
```

### Sprites
```
sprite $businessProcess [16x16/16] {
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFF00FFFF
FF00000000000FFF
FF000000000000FF
FF00000000000FFF
FFFFFFFFFF00FFFF
FFFFFFFFFF0FFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
}
rectangle "inner process 1" <<$businessProcess>> as src
```


## Formatting
https://plantuml-documentation.readthedocs.io/en/latest/formatting/all-skin-params.html
