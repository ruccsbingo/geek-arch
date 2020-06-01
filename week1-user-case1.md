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

![](http://www.plantuml.com/plantuml/png/XO_FIiGm4CRlynHpr4DzW2AoRoB3Tgo5D8LaWWSHl2YB82WYx46GWdWi7XP5nRUnVnx3fabXOG_c4lZDz_qoMLWX8wvK08fF1AL2K-IdWbbXU2b5fG7IxdqrR3w7owiKoUAoqjQLR4R-TDlUrEtzUk9dL8YdVLFtTzSpBKbJFcBmEjAvOZHiXPmXBNWEE9wzOVFQhJv2SN-hTUpVgXI7rE_NIxT-cEPYA8iqBjUyjJ-F_VVpqDHJmWe9N03CssAI7ErejuV1YH2kmoJ1-KUnvKD16pC7Eq9CqLa67_f_6YI1mO9rvahr1m00)



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

![](http://www.plantuml.com/plantuml/png/ROyzRiKW3CTtdy8NU4iFKBqxTAogo08dHGKxDMR8xHlIWUGfBF3_-0aRdjN9l9KCcMT7LxIqV3l6P1mygK3zIRAIKS6WPLLXyG_VCkCElG4aSRQP0gCRHSQJyTlOjgawEG3kPoJ6IwhEXiC_4HI2Dlc7HlM1duM45hOfg5JD_DKBL-Qs1STaFJeUKz7Okd-L-7X__NyiqE5-3tQeE_J94bl9Vm00)

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



![](http://www.plantuml.com/plantuml/png/SoWkIImgAStDuKf9B4bCIYnELL3AhImkp55II2nMI37auihBJm6AFPkoxTcQVS_cx59IgEPI089eY4WiLorCoVDr2vzFQ7iweUzf_mQmxZn3cDhSnBp4zDIY-EJylEBydDHOY6X9KM9AQdnkVaefN0ZecXAe2DXac2qAkdRe6XIi53n2GWAuyWo1ac2NSZcavgK0lG80)


@startuml

:用户: as user1

rectangle control {
    (按数字按钮) as digital
    (显示号码) as display
    (扬声器发音) as speaker
    (按发送按钮) as send 
    (接通无线网络) as connect
    (拨号) as dial
}

user1 -> digital
digital .> display : use
digital .> speaker : use
user1 -> send
send .> connect : use
send .> dial : use


@enduml

![](http://www.plantuml.com/plantuml/png/SoWkIImgAStDuUAoUZvbnREExLOAYSKAfSMfHOPSN4MfoIM9UUavgGh9-NabHVav2jLS2a2WyQodyzdK3K_NJWSoNavQfmdIavAPdbcIc0DLC6FVyoMxdlPlVxwW4IfRN92JM0cLxLppTF66fpDNFEsV-7B-Ph22ueBKnEpK8hZv8Ac6HYJpYrFpKXIWqdrBNpRCUZPzmVDT-v_ldVXyznoG2f0Zyu0kXghfNW6q7cetq5crN5nWNodesi6T2gKLzEnWxbEm0laTIGBcBeW4t0YmQxX0150Dp6A86fWes5ge41UN0r0G6Cm0)

https://www.ibm.com/developerworks/cn/rational/rationaledge/content/feb05/bell/bell.html

https://blog.anoff.io/2018-07-31-diagrams-with-plantuml/
