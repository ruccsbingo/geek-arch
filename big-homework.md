@startuml
left to right direction
actor "用户" as user
actor "骑手" as courier

package deliverySys {
    usecase "用户下单" as order
    usecase "用户支付" as pay
    usecase "快递员上报地理位置" as uploadGEO
    usecase "向距离用户直线距离5km内的所有快递员发送通知" as notifyNewOrder
    usecase "快递员抢单" as grapOrder
    usecase "快递员到用户处收取快递" as receiveCourier
    usecase "快递员将快递送到目的地" as delivery

    usecase "第一个抢单的快递员得到配单" as firstTakeOrder
    usecase  "系统向其发送用户详细地址" as pushUserAdress
    usecase "记录到系统" as logSystem
}

user --> order
user --> pay
courier --> uploadGEO
courier <-- notifyNewOrder
courier --> grapOrder
courier --> receiveCourier
receiveCourier --> logSystem
courier --> delivery
delivery --> logSystem

grapOrder --> firstTakeOrder
firstTakeOrder --> pushUserAdress
courier <-- pushUserAdress

@enduml

@startuml
|用户|
start
:用户下单;
:下单成功后支付;
|#AntiqueWhite|系统|
:获取用户5KM内的快递员;
:向5KM内的快递员推送订单信息;
|快递员|
:收到系统推送的新订单信息;
:抢单;
|系统|
:向第一个抢成功的快递员返回用户地址;
|快递员|
:快递员取货;
:录入系统;
:快递员配送;
:录入系统;
stop
@enduml

@startuml
agent agent [
    ios/android
]
cloud dns
node gateway [
    nginx
    ----
    192.10.1.11
    192.10.1.12
]
node service [
    core-service
    ----
    192.10.2.11
    192.10.2.12
]
node cache [
    redis-cluster
    ----
    192.10.4.10
    192.10.4.11
]

node mq [
    kafka
    ----
    192.10.5.10
    192.10.5.11
]
node storage [
    hadoop
    ----
    192.10.6.10
    192.10.6.11
    ....
    hdfs,spark,flink
]
database master [
    core
    shardDB
    ----
    192.10.3.10
    192.10.3.11
    ....
    postgres
]
database slave [
    core
    shardDB
    ----
    192.10.3.10
    192.10.3.11
    ....
    postgres
]

agent -- dns : http/internet
agent -- gateway : http/internet
gateway -- service : http/lan
service -- cache : tcp/lan
service -- mq : tcp/lan
mq -- storage : tcp/lan
service -- master : write(tcp/lan)
service -- slave : read(tcp/lan)
master .. slave : copy
@enduml

@startuml

@enduml