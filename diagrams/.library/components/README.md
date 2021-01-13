# How to create a component in a library

## Describe component

```plantuml
@startuml (id=component)

component "Component name" as component-variable <<component>>

@enduml 
```

Change the component name, `component-variable` and component stereotype as required.
You can keep the `<<component>>` stereotype if you don't have another.

## Describe what interfaces the component provides

```plantuml
@startuml (id=interfaces)

!include .component-tamplate.puml

!startsub getCollection

    interface "GET /collection" as getCollection
    ComponentVariable --() getCollection

!endsub

!startsub postCollection

    interface "POST /collection" as postCollection
    ComponentVariable --() postCollection

!endsub

@enduml
```

Use right component file name in `!include`.

Add provide interface to `!startsub` block.
Use a personal `!startsub` block for each interface.

## Describe what interfaces the component required

```plantuml
@startuml (id=required-interfaces)

!include .component-tamplate.puml

!includesub <./path/to/other-component.puml>!requiredInterfaceVariable

!startsub requiredInterfaceVariable
    
    ComponentVariable -up-( requiredInterfaceVariable

!endsub

!startsub requiredInterfaceLocal
    
    interface "GET /external-collection" as requiredInterfaceLocal
    ComponentVariable -up-( requiredInterfaceLocal

!endsub

@enduml
```

Use right component file name in `!include`.

Include required interface other component as Variable use `!includesub` or create local.
