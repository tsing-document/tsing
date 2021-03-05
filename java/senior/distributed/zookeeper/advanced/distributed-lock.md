![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distributed/zookeeper/advanced/distributedlockjava-senior-distriuted-zookeeper-%E8%BF%9B%E9%98%B6%E7%AF%87-%E5%88%86%E5%B8%83%E5%BC%8F%E9%94%81.png)

# 目录
- 分布式锁
- zookeeper分布式锁
- 注意事项

## 1、分布式锁
分布式锁是控制分布式系统之间同步访问共享资源的一种方式。

## 2、zookeeper分布式锁
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distributed/zookeeper/advanced/distributedlockjava-senior-distriuted-zookeeper-%E8%BF%9B%E9%98%B6%E7%AF%87-%E5%88%86%E5%B8%83%E5%BC%8F%E9%94%81-lock-update.png)
- ① 客户端A创建临时顺序节点`demo`。并在节点下创建`x_00000001`。
- ② 客户端A判断是否自己是第一个节点，如果是就锁成功。
- ③ 客户端B创建临时顺序节点`demo`。 并在节点下创建`x_00000002`。
- ④ 客户端B判读是否自己是第一个节点，如果是第一个节点，就加锁成功。如果不是第一个节点就会创建第二个节点，然后创建一个监听器，监听上一个节点。
- ⑤ 客户端A执行完业务逻辑之后，会释放锁，并且会删除顺序节点`x_00000001`。
- ⑥ zk服务器会通知客户端B，上级节点已经删除了。
- ⑦ 客户端B会重新加锁。 

## 3、注意事项
用临时顺序节点，如果某个客户端创建临时节点之后，不小心自己宕机了，zk服务器感知到那个客户端宕机了，会自动删除对应的顺序节点。

<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。


