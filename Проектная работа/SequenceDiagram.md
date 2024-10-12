```puml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Sequence.puml

Person(user, "Operator")
Container(mes, "MES", "#NET")
Container(mes_api, "MES API", "SpringBoot")
Container(cache, "Cache", "_")
Container(crm_db, "CRM DB", "PostgreSQL")
Container(rabbit, "RabbitMQ", "Erlang")

Rel(crm_db, cache, "Updates orders cache", "Pass Order entities")
Rel(user, mes, "Clicks on orders page button")
Rel(mes, mes_api, "Requests orders list", "JSON/HTTPS")
Rel(mes_api, cache, "Fetches orders", "JSON/HTTPS")
Rel(cache, mes_api, "Returns orders", "JSON/HTTP")
Rel(mes_api, mes, "Returns orders", "JSON/HTTP")
Rel(mes, user, "Draw list")

Rel(user, mes, "Assigns order")
Rel(mes, mes_api, "Requests to update state", "JSON/HTTPS")
Rel(mes_api, cache, "Saves new state", JSON/HTTPS)
Rel(cache, crm_db, "Writes new state", "SQL")
Rel(crm_db, cache, "Confirm write operation")
Rel(cache, cache, "Updates states")
Rel(cache, mes_api, "Returns result", JSON/HTTPS)
Rel(mes_api, rabbit, "Sends event about state changed")
Rel(mes_api, mes, "Returns write result", JSON/HTTPS)
Rel(mes, user, "Update state", "JSON/HTTP")

SHOW_LEGEND()
@enduml
```