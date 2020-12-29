---
id: 35a22ebd-29ee-4ecf-8068-74347c4578b7
title: Puml
desc: ''
updated: 1609278199564
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