1. 根据微服务框架dubbo的架构图，画出dubbo进行一次微服务调用的时序图。

@startuml
participant Consumer
participant Registry
participant Provider
Registry <- Provider : Provider注册到Registry
Consumer -> Registry : Consumer拉取Provider信息
Consumer -> Consumer : 通过代理对象 Proxy 发起远程调用
Consumer -> Consumer :通过网络客户端 Client发送请求
Consumer -> Provider : Transpoter编码序列化,调用provider
Provider -> Provider : 对数据包进行解码
Provider -> Provider : 将解码后的请求发送至分发器 Dispatcher
Provider -> Provider : 分发器将请求派发到指定的线程池上
Provider -> Provider : 线程池调用具体的服务
Consumer <- Provider : 返回结果
@enduml

![](http://www.plantuml.com/plantuml/png/TP9HJl9G48NVkueku6S3VumXmGKOumOQQBG9bAOjHjv0fLGe0W4nGaEeFDZ4X9QWgOBOpNJklUp2IsghVUXJ9wVdV3DtCanMKJbPhPIAZ4I_GbwGE55bSsLHgPHuEI6Uy6U2eihLX7Wibo-40dL6Vzc3J2oo_-CIhMpG3D3Tc1BrO3E7CPe68XcrRw4xYkA1Rw6wayX4DStiQcFYDuFD7FSqS3x8qjhtlQooqEsJDu_u9hRRnBt6Gpi54HBmjeyt9YoUaExX5uVD5GLUL2baLwiJnqFBgqJyppDFPKvKfBBAo_XpX6TrM7T1Vm1Zz2ziAqLhYZF9F9qQtRkeim2ZGVm9iGpoFAUSLB-hXGRetU7nJJZSpw3D5UWQhU7HPey4HUBK_7bwvzXBaI46lNxj5Tr5HXCMOuh7Qvyk42rdmNihZHDxmWT3mmks0vf5PWTQrk_UakT1_25CfdWpG5EJoV9YON-9p3S0)
