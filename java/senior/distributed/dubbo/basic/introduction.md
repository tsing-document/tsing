![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/dubbo/basic/introduction/java-senior-distriuted-dubbo%E5%9F%BA%E7%A1%80%E7%AF%87-%E4%BB%8B%E7%BB%8D.png)

# 目录
- 概述
- 六大核心
- 官网地址
- 网站应用演进
- Dubbo架构
- Dubbo特点

## 1、概述    
Apache Dubbo 是一款高性能、轻量级的开源 Java 服务框架。  


## 2、官网地址
`官网地址：` **https://dubbo.apache.org/**  

## 3、六大核心
`Apache Dubbo 提供了六大核心功能`：
- 面向接口代理的高性能RPC调用。
- 智能容错和负载均衡。
- 服务自动注册和发现。
- 高度可扩展能力。
- 运行期流量调度。
- 可视化的服务治理与运维。

## 4、网站应用演进
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/dubbo/basic/introduction/java-senior-distriuted-dubbo%E5%9F%BA%E7%A1%80%E7%AF%87-%E4%BB%8B%E7%BB%8D-evolution.png)
> 1、单一应用架构

当网站流量小的时候，单一的应用会将我们的业务的增删改查包含到一个项目中，这样有助于我们进行项目代码编写、项目的部署。

> 2、垂直应用架构

当网站流量增加的时候，我们会将应用根据业务分为不同的项目，这样我们的开发人员可以根据业务分组进行编写业务代码。

> 3、分布式应用架构

当业务的复杂度变高了，垂直应用的架构之间会出现服务交叉调用，这个时候就可以将核心的业务抽取出来作为核心的服务。

> 4、面向服务的架构

当服务之间调用变得多了，服务之间的关系我们就会难以管理，也不能通过图形化页面只管的看出来。

## 5、Dubbo架构
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/dubbo/basic/introduction/java-senior-distriuted-dubbo%E5%9F%BA%E7%A1%80%E7%AF%87-%E4%BB%8B%E7%BB%8D-dubbo-architecture.png)

> 节点说明

| 节点 |  角色说明   |
| --- | --- |
| Consumer    |  服务消费者  |
| Registry    |  注册中心   |
| Monitor    |   监控中心  |
| Provider    |  服务提供者   | 
| Container |  服务运行容器   |

## 6、Dubbo特点
Dubbo具有以下特点：连通性、健壮性、伸缩性、升级性。




<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。


