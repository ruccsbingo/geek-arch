@startuml
autonumber
participant 应用服务器  as app 
participant 管理服务器 as config
participant "存储服务（序列1服务器NO.2）（故障）" as store1
participant "存储服务（序列2服务器NO.2）" as store2
participant 临时服务器 as tmp
config -> config : 服务器故障，更新集群路由信息
app -> config : 获取集群路由信息
app -> store2 : 读数据（只从正常服务器读）
app -> store2 : 写数据
app -> tmp : 故障服务器恢复服务前，写入数据
store1 <- tmp : 故障服务器恢复后，从临时挂起迁移故障期间写入的数据
app -> store1 : 迁移完成，恢复正常写入 
app -> store2 : 迁移完成，恢复正常写入 
@enduml


![](http://www.plantuml.com/plantuml/png/ZPBVIW915CRlzoa6xmtqKY9yWdg6pIo4N0ST7q19qN3L2__a7mZBI0B_19QYaY_ZcTczyXKwoumRGnJUpSvyl-zyts6Z6MQcMJPvQvXPbhAooSjusg1ubOWbg6an0gk6Q8nutuRx0NH6X9WPOb9AD96O34Izw8iyJInbNITkD5K0nW-GLrxxJGbMDIYrGpvsVd4Itc_A-CAR1RVRntF0iygmL3eUEi8gh5bfU5Z3TyivRtzgULcI6Z8p2PuHTOeGNtE8LE6zEM_Dt5vHV0sTnLGqtdVR0SzD3PDI3NMg2wYr_XRAN9vmkkRD6RSdNf7QssvTvUDdM2xzsIZ0ChyuA7Oafrwy3dWja_u4ppt1q5QVPHiR80U55uNAvPBJu7yqrAl8OJ2rk4hU-LWusvnuNH_qZsvxBer5zqwFfKP4Y2HWKk6bElf9RzbLeaJlU1mIZLjN-0D_0m00)
