#### 架构

- 概要：
    - Dubbo架构：
        -  ![Dubbo架构](./img/dubbo-architecture.jpg)
    - 整体架构分层：
        - 接口服务层（service）:
            - 该层和业务逻辑相关，根据provider和consumer业务设计对应的接口和实现。
        - 配置层（Config）:
            - 对外配置接口，以serviceConfig 和 refererceConfig为中心。
        - 服务代理层（Proxy）：
            - 服务接口透明代理，生成服务的客户端Stub和服务端的Skeleton，以ServiceProxy为中心，扩展接口为ProxyFactory。
        - 服务注册层（Registry）:
            - 封装服务地址的注册和发现，以服务URL为中心，扩展接口为RegistryFactory、Registry、RegistryService。
        - 路由层（Cluster）：
            - 封装多个提供者的路由和负载均衡，并桥接注册中心，以Invoker为中心，扩展接口为Cluster、Directory、Router、LoadBlancce。
        - 远程调用层（Protocal）：
            - 封装RPC调用，以Invocation和Result为中心，扩展接口为Protocal、Invoker和Exporter。
        - 信息交换层（Exchange）：
            - 封装请求响应模式，同步转异步。以Request和Response为中心，扩展接口为Exchanger、ExchangeChannel、ExchangeClient和ExchangeServer。
        - 网络传输层（Transport）：
            - 抽象mina和netty为统一接口，以Message为中心，扩展接口为Channel、Transporter、Client、Server、Codec。
        - 数据序列化层（Serialize）：
            - 可复用的一些工具，扩展接口为 Serialization、ObjectInput、ObjectOutput和ThreadPool。
    - 角色说明：
        | 节点 | 角色说明 |
        | :-----|:---- |
        | Provider | 暴露服务的服务提供方 | 
        | Consumer | 调用远程服务消费方 |
        | Registry | 服务注册和发现的注册中心 |
        | Moitor | 统计服务的调用次数和调用时间的监控中心 |
        | Container | 服务运行容器 |
    - Dubbo特点：
        - 连通性
        - 健壮性
        - 伸缩性
        - 升级性
- 语法：
- 案例：
