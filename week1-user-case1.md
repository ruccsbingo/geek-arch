@startuml

left to right direction

:消费者: as consumer
:服务员: as waiter
:管理员: as manager

rectangle restaurant {
    (账户管理) as manager_console
    (交易) as trade
    (消费记录统计) as stat
}

consumer --> manager_console
consumer --> trade 
trade <--  waiter
manager --> stat

trade .> manager_console : use
stat .> manager_console : use
stat .> trade : use

@enduml




@startuml
left to right direction
skinparam componentStyle uml2

interface trade 
interface query_stat

    interface register 
    interface query_account

    register - [manager_console]
    query_account - [manager_console]

trade - [trade_module]
[trade_module] -> query_account

query_stat - [stat_module]
[stat_module] -> query_account
@enduml

@startuml
database "mysql" as d1

node "收款机" {
    [收款]
}

node "管理后台" as n1 {
    [manager_console]
    [trade_module]
    [stat_module]
}

[收款] ->  [trade_module] : HTTP
n1 -> d1


@enduml


https://www.ibm.com/developerworks/cn/rational/rationaledge/content/feb05/bell/bell.html

https://blog.anoff.io/2018-07-31-diagrams-with-plantuml/
