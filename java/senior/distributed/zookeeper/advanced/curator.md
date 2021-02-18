![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/zookeeper/advanced/curator/java-senior-distriuted-zookeeper-%E8%BF%9B%E9%98%B6%E7%AF%87-curator.png)

# 目录
- 概述
- 添加依赖
- 创建连接
- session重连策略
- 创建节点
- 修改节点
- 删除节点
- 查看节点
- 查看节点是否存在
- 事务

## 1、概述    
[Curator](https://curator.apache.org/)是`Netflix`开源的一套zookeeper客户端框架。解决原生Api的好多问题。

## 2、添加依赖
```java
       <!-- 对zookeeper的底层api的一些封装 -->
        <dependency>
            <groupId>org.apache.curator</groupId>
            <artifactId>curator-framework</artifactId>
            <version>2.12.0</version>
        </dependency>
        <!-- 封装了一些高级特性，如：Cache事件监听、选举、分布式锁、分布式Barrier -->
        <dependency>
            <groupId>org.apache.curator</groupId>
            <artifactId>curator-recipes</artifactId>
            <version>4.0.0</version>
        </dependency>
```


## 3、创建连接
```java
package com.snails.curator;

import org.apache.curator.framework.CuratorFramework;
import org.apache.curator.framework.CuratorFrameworkFactory;
import org.apache.curator.retry.ExponentialBackoffRetry;
import org.apache.curator.retry.RetryNTimes;
import org.apache.curator.retry.RetryOneTime;
import org.apache.curator.retry.RetryUntilElapsed;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

public class CuratorConection {

    private String IP = "127.0.0.1:2181";
    CuratorFramework curatorFramework = null;

    @Before
    public void brfore() {
        ExponentialBackoffRetry exponentialBackoffRetry = new ExponentialBackoffRetry(1000, 3);
        curatorFramework = CuratorFrameworkFactory.builder()
                                //IP地址端口号
                                .connectString(IP)
                                //会话超时时间
                                .sessionTimeoutMs(5000)
                                //重连机制
                                .retryPolicy(exponentialBackoffRetry)
                                //命名空间
                                .namespace("create")
                                //构建连接对象
                                .build();

        curatorFramework.start();

        System.out.println(curatorFramework.isStarted());
    }

    @After
    public void after() {
        curatorFramework.close();
    }

    @Test
    public void test() {}

}


```
## 4、session重连策略
> 1、3秒后重连一次，只重连一次
```java
  new RetryOneTime(3000)
```

> 2、每3秒重连一次，重试3次
```java
  new RetryNTimes(3, 3000)
```

> 3、每3秒重连一次，总等待时间超过10秒后停止重连
```java
  new RetryUntilElapsed(1000, 3000)
```

> 4、根据公式获取重试时间 baseSleepTimeMs * Math.max(1, random.nextInt(1 << (retryCount +1)))
```java
  new ExponentialBackoffRetry(1000, 3)
```

## 5、创建节点
```java
    @Test
    public void create01() throws Exception {
        curatorFramework.create()
                //节点类型
                .withMode(CreateMode.PERSISTENT)
                //节点权限列表
                .withACL(ZooDefs.Ids.OPEN_ACL_UNSAFE)
                //会加上命名空间指定的名称
                .forPath("/tsing", "测试数据".getBytes());
        System.out.println("end");
    }

    //自定义权限列表
    @Test
    public void create02() throws Exception {
        ArrayList<ACL> list = new ArrayList<>();

        Id id = new Id("ip", "127.0.0.1");
        list.add(new ACL(ZooDefs.Perms.ALL, id));
        curatorFramework
                .create()
                .withMode(CreateMode.PERSISTENT)
                .withACL(list)
                .forPath("/tsing1", "tsing1".getBytes());

    }

    //递归创建节点
    @Test
    public void create03() throws Exception {
        curatorFramework
                .create()
                .creatingParentContainersIfNeeded()
                .withMode(CreateMode.PERSISTENT)
                .withACL(ZooDefs.Ids.OPEN_ACL_UNSAFE)
                .forPath("/tsing2/child1", "tsing2".getBytes());
    }
```

## 6、修改节点
```java
    @Test
    public void set01() throws Exception {
        curatorFramework
                .setData()
                .forPath("/nodo", "set-node-update".getBytes());
        System.out.println("end");
    }
```

## 7、删除节点
```java
    @Test
    public void delete01() throws Exception {
        curatorFramework
                .delete()
                .forPath("/node");
    }
    
    //删除包含子节点的节点
    @Test
    public void delete02() throws Exception {
        curatorFramework
                .delete()
                .deletingChildrenIfNeeded()
                .forPath("/node");
    }
```

## 8、查看节点
```java
    @Test
    public void get01() throws Exception {
        byte[] bytes = curatorFramework
                .getData()
                .forPath("/node");

        System.out.println(new String(bytes));
    }
    
    //查看子节点数据
    @Test
    public void get02() throws Exception {
        List<String> list = curatorFramework
                .getChildren()
                .forPath("/node");

        for (String str : list) {
            System.out.println(str);
        }
    }
```

## 9、查看节点是否存在
```java
    @Test
    public void exists01() throws Exception {
        Stat stat = curatorFramework
                .checkExists()
                .forPath("/node");

        System.out.println(stat.getVersion());
    }
```

## 10、事务
```java
    @Test
    public void set01() throws Exception {
        curatorFramework
                //开启事务
                .inTransaction()
                .create().forPath("/node3", "node3".getBytes())
                .and()
                .setData().forPath("/node4", "node4".getBytes()).and()
                //提交事务
                .commit();
                
        System.out.println("end");
    }
```

<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。


