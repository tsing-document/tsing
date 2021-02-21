![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/dubbo/basic/usageexample/java-senior-distriuted-dubbo-%E5%9F%BA%E7%A1%80%E7%AF%87-%E7%94%A8%E6%B3%95%E7%A4%BA%E4%BE%8B.png)

# 目录
- 启动时检查
- 集群容错
- 负载均衡
- 直连提供者

## 1、启动时检查
默认值是`check="true"`。web项目启动时默认会检查依赖项目是否可用，不可用时出现异常，会阻止spring初始化完成。

> 1、配置文件关闭
```java
  <dubbo:reference interface="com.foo.BarService" check="false" />
```

> 2、注解方式关闭
```java
  @Reference(check = false)
```

## 2、集群容错

> 1、failover cluster 默认

失败自动切换，当出现失败，重试其他服务器。通常用于读操作，但重试会带来更长延迟。可用`retries=2`来设置重试次数（不含第一次）。

**配置方式：**  
```java
  <dubbo:service retries="2" />
  或者
  <dubbo:reference retries="2" />
```

> 2、failfast cluster

快速失败，只发起一次调用，失败立即报错。通常用于非幂等性的写操作，比如新增记录。

> 3、failsafe cluster

失败安全，出现异常时，直接忽略。通常用于写入审计日志等操作。

> 4、failback cluster

失败自动恢复，后台记录失败，定时重发。通常用于消息通知操作。

> 5、forking cluster

多个服务器，只要有一个成功就直接返回。通过`fork="2"`来设置。

> 6、broadcast cluster

广播调用所有提供者，逐个调用，任意一台报错就报错。

> 7、配置方式
```java
    <dubbo:service cluster="failsafe" />
    或者
    <dubbo:reference cluster="failsafe" />
```

## 3、负载均衡
> 1、random loadbalance

`随机`,按权重设置随机概率。

> 2、roundrobin loadbalance

`轮询`,按公约后的权重设置轮询比率。  
 **问题：**
如果轮询到的一台机器上的服务出现异常，这个时候会出现消息堆积的现象。

> 3、leastactive loadbalance

`最少活跃数`相同活跃数的随机，活跃数指调用前后计数差。

> 4、consistenHash loadbalance
`一致性hash`，相同参数的请求总是发到同一个提供者。

> 5、配置方式
```java
  # 服务端服务级别
  <dubbo:service interface="..." loadbalance="roundrobin" />

  # 客户端服务级别
  <dubbo:reference interface="..." loadbalance="roundrobin" />

  # 服务端方法级别
  <dubbo:service interface="...">
    <dubbo:method name="..." loadbalance="roundrobin"/>
  </dubbo:service>
  
  # 客户端方法级别
  <dubbo:reference interface="...">
    <dubbo:method name="..." loadbalance="roundrobin"/>
  </dubbo:reference>
```

## 4、直连提供者
不通过注册中心直接连接服务提供者。如果你的项目已经整合dubbo和zookeeper，用下面的方式测试直连服务提供者。

> 1、启动zookeeper

> 2、启动服务提供者

> 3、关闭zookeeper

> 4、注解方式配置
```java
@RestController
@RequestMapping(value = "/demo")
public class DemoController {

    @Reference(check = false, url = "dubbo://localhost:20880")
    private DemoService demoService;

    @RequestMapping(value = "/healthy")
    public String healthy() {
        return demoService.healthy();
    }
}
```

> 5、启动消费者

> 6、访问连接


<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。


