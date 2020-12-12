#### 常见问题：

- 概要：
    - 集群容错：
        - 定义：
            - 当集群调用失败时，Dubbo提供了多种容错方案，默认时 failover 重试。
        - 分类：
            - Failover Cluster：
                - 失败自动切换，当出现错误，重试其他服务器。重试2次，不算第一次访问。
            - Failfast Cluster：
                - 快速失败，只发起一次调用，失败立即报错。
            - Failsafe Cluster：
                - 失败安全，出现异常时，直接忽略。
            - Failback Cluster：
                - 失败自动恢复，后台记录失败请求，定时重发。
            - Forking Cluster:
                - 并行调用多个服务器，只要一个成功就返回。
            - Broadcast Cluster：
                - 广播调用所有的提供者，逐个调用，任意一台报错则报错。
    - 负载均衡：
        - 定义：
            - 在集群负载均衡时，Dubbo提供了多种负载均衡，默认是 random 随机调用。
        - 分类：
            - Random LoadBalance（随机）：
                - 按权重设计随机概率。
            - RoundRobin LoadBalance（轮询）：
                - 按公约后的权重设置轮询比率。这个会出现问题，比如：第二台机器很慢，当请求到第二台机器时，时间长了，所有的请求都会卡在第二台。
            - LeastActive LoadBalance（最少活跃用数）：
                - 当请求调用少的机器越容易被调用到。
            - ConsistentHash LoadBalance（一致Hash）:
                - 相同参数的请求总是发送到同一个提供者。
    - 线程模型：
        - TODO:
    - 多协议：
        - TODO:
    - 隐式参数：
        - 消费方设置
            ```java
                RpcContext.getContext().setAttachment("index", "1");
            ```
        - 服务方获取
            ```java
                String index = RpcContext.getContext().getAttachment("index"); 
            ```
    - 事件通知：
        - 在调用之前、之后、出现异常时通知
    - Dubbo的注册中心集群挂掉之后，发布者和订阅者之间还能通信吗？
        - 可以通讯，启动Dubbo时，消费者会从zookeeper拉取注册的生产者的地址接口等数据，缓存在本地，每次调用时，按照本地存储的地址进行调用。
- 语法：
- 案例：
