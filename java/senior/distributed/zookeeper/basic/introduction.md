![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/zookeeper/basic/zookeeper-%E5%9F%BA%E7%A1%80%E7%AF%87-%E4%BB%8B%E7%BB%8D.png)

# 目录
- Zookeeper 简介
- Zookeeper 数据结构
- cap 理论 
- base 理论

## 1、Zookeeper 简介
在过去，每个应用程序都是运行在一台计算机上的单程序单CPU。今天，情况变了。在大数据和云计算领域，应用程序是由运行在不断变化的计算机上的许多独立程序组成的。程序员不能够专注编写业务代码，反而要花费大量的时间维护各个服务之间的关系。为了解决程序员能够专注于业务代码的实现，zookeeper相关的应用`应世而生`。  

它支持分布式系统的调度任务，协调任务是涉及多个进程的任务。这样的任务是可以为了合作是为了规范争论。合作意味着各个进程需要共同努力，而主进程采取行动使其他进程能够正常运行。例如：在典型的主从架构中，主通知从进行工作。因此，主人可以分配任务给园丁。但是，我们确实希望有一个主进程，但是每个子进程又能称为主进程，因此，多个进程需要实现互斥。

一个典型的分布式数据一致性的解决方案，分布式应用程序可以基于它实现诸如数据发布/订阅、负载均衡、命名服务、分布式协调/通知、集群管理、Master 选举、分布式锁和分布式队列等功能。

## 2、Zookeeper 数据结构
zookeeper提供的名称空间非常类似于标准文件系统，key-value的形式存储。名称key由`/`分割的一系列路径元素，zookeeper名称空间中的每个节点都是一个路径标识。
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/zookeeper/basic/java-senior-distriuted-zookeeper-%E5%9F%BA%E7%A1%80%E7%AF%87-%E4%BB%8B%E7%BB%8D-node.png)

## 3、cap 理论
> `一致性（Consistency）`:在分布式环境中，一致性是指多个副本之间是否能够保持一致的特性，等同于所有节点访问同一 份最新的数据副本。在一致性的需求下，当一个系统在数据一致的状态下执行更新操作后，应该保证系统数据依然处于一致的状态。  
> `可用性（Availability）`:每次请求能获取到正确的响应，但是不保证获取的数据为最新数据。  
> `分区容错性（Partition tolerance）`:分布式系统在遇到任何网络分区故障的时候，依然要能够保证提供满足一致性和 可用性的服务，除非整个网络环境都发生了故障。  

> 但是一个分布式系统中最多只能满足两点：`分区容错性（Partition tolerance）`是必须的。
> zookeeper是满足了CP。
> SpringCloud中的eruka实现了AP。

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/zookeeper/basic/java-senior-distriuted-zookeeper-%E5%9F%BA%E7%A1%80%E7%AF%87-%E4%BB%8B%E7%BB%8D-cap.png)

## 4、base 理论
1. 基本可用（Basically Available）
2. 软状态（Soft State）
3. 最终一致性（Eventually Consistent）

> 基本可用（Basically Available）:
- 1、`响应时间上损失`：正常情况下的搜索引擎0.5秒后就返回给用户结果，而基本可用的搜索引擎可以在2秒作用返回结果。  
- 2、`功能损失`：在正常情况下，用户可以顺利完成每一笔订单。但是到了大促销期间，为了保证购物系统的稳定性，可以将其他服务引导到降级页面。

> 软状态（Soft State）:
- 1.硬状态是指所有节点的数据副本的数据必须完全一致。软状态是允许系统在多个不同节点的数据副本可以存在数据延时。

> 最终一致性（Eventually Consistent）:
- 最终一致性又分为以下5种：  
  - 因果一致性（Causal consistency）   
  - 读己之所写（Read your writes）   
  - 会话一致性（Session consistency）  
  - 单调读一致性（Monotonic read consistency）  
  - 单调写一致性（Monotonic write consistency） 
  
  
<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。
