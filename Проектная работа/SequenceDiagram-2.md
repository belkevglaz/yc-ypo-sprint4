```puml
@startuml
!theme C4_united from https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/themes
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Sequence.puml

Person_Ext(Alice, "Alice")
Person(Bob, "Bob")

activate Bob

Rel(Alice, Bob, "Authentication Request")

alt successful case
    Rel(Bob, Alice, "Authentication Accepted")
else some kind of failure
    loop 1000 times
        Rel(Alice, Bob, "DNS Attack")
    end
end

ref over Alice, Bob : init

Rel(Alice, Bob, "hello")

ref over Bob
  This can be on
  several lines
end ref

== Initialization ==

Rel(Alice, Bob, "Authentication Request")
Rel(Bob, Alice, "Authentication Response")

== Repetition ==

Rel(Alice, Bob, "Another authentication Request")
Rel(Bob, Alice, "another authentication Response")

... 5 minutes later ...

Rel(Alice, Bob, "calls via phone")

SHOW_LEGEND()
@enduml
```