![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distributed/zookeeper/advanced/custerfontimage.png)

# 目录
- 1、概述
- 2、集群选取机制
- 3、搭建过程

## 1、概述
> 1、集群架构图

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distributed/zookeeper/advanced/custercluster.png)

> 2、集群中的角色

`Leader：`Zookeeper集群工作的核心，事务请求（写操作）唯一调度和处理者，保证集群事务处理的顺序性；集群内部各个服务的调度者。对于 **create、setData、delete**等有些操作的请求，则需要统一转发给Leader处理，Leader需要决定编号、执行操作，这个过程称为一个事务。

`Follower：`处理客户端非事务（读操作）请求，转发事务请求给Leader, 参与Leader选取投票。

`Observer：`观察者角色，观察zookeeper集群的最新状态变化并将状态同步过来，其对于非事务的请求可以进行独立处理，对于事务请求，则会转发给Leader服务器处理，不会参数任何形式的投票只提供服务，其实就是增加非事务的并发量。

> 2、集群为什么要搭建奇数个节点
- 如果部署单个节点，当节点宕机时，集群就会失效，就会出现单点故障。
- 如果部署两个节点，2的半数为1，半数以上最少为2，不允许有一台机器故障，不然投票机制不成立。
- 如果部署三个节点，3的半数为1.5，半数以上最少为2，允许有一台机器故障，投票机制可以成立。
- 如果部署四个节点，4的半数为2，半数以上最少为3，允许有一台机器机器故障，投票机制可以成立。
- 如果部署五个节点，5的半数为2.5，半数以上最少为3，允许有两台机器故障，投票机制可以成立。
- 所以部署zookeeper集群的时候一般部署的节点数量为`2n+1`台节点。

## 2、集群选取机制
> 1、节点状态

| 名称 |  描述  |
| --- | --- |
| Looking | 这个是在选举的过程中的状态，正在选举。|
| Leading | 领导者状态，说明当前节点角色已经是Leader。|
| Following | 跟随者状态，表示选举已经完成，当前角色已经是Following。|
| Oberver | 观察者状态，表示当前节点角色是observer。|

> 2、事务ID

Zookeeper状态每次变化都接收一个`ZXID`（zookeeper事务id）形式的标记，由Leader统一分配，全局唯一，不断递增。

> 3、初始化选取过程

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distributed/zookeeper/advanced/custerinit.png)

由三个节点举例：当`第一个节点`启动的时候，因为单节点无法进行选举，所以当`第二个节点`启动之后，两台机器之间可以互相通信了，开始选举过程：

- 1、两个节点都当自己是Leader角色来投票，每次投票都包含服务器配置的`myid`（下文中能找到myid）中的值和`ZXID`。使用`(myid, zxid)` 表示，此时第一个节点为`(1, 0)`，第二个节点为`(2, 0)`，然后将自己的值发给其他节点。
- 2、当其他服务收到投票后，先判断是否是本轮投票，投票的机器的状态是否为`Looking`。
- 3、针对每次的投票，服务器都需要将自己的票数和其他服务器对比。先检查`ZXID`，这个时候`ZXID`都为0，如果`ZXID`谁的大谁就是Leader，如果`ZXID`相同就对比`myid`，第二个节点的`myid`为2，所以第二个节点就是Leader。
- 4、每次投票之后，服务器会统计是否有过半的机器接收到相同的投票信息，如果已经过半，就确认第二个节点为Leader。
- 5、一旦确认了Leader，每台服务器都会更新自己的状态。如果是`Follower`角色，就改变状态为`Following`，如果是`Leader`角色，就改变状态为`Leading`。当`第三个节点`进来的发现已经有了Leader,状态直接变成`Following`。

> 4、运行状态下选举

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distributed/zookeeper/advanced/custerrunning.png)

以下当第二个节点故障，第一个节点和第三个节点是良好的节点。

- 1、当Leader挂掉之后，集群会拒绝所有的服务，余下非`Observer`服务器都会将自己的服务器的状态变更为`Looking`。然后开始选举。
- 2、每个节点会发出投票。运行期间，节点上的`ZXID`可能不同，假设：第一个节点的`ZXID`为100，第三个节点的`ZXID`为120，这个时候第一个节点和第三个节点都会投票自己，第一个节点为`(1, 100)`，第三个节点为`(3, 120)`，由于第三个节点的`ZXID`为120，直接选举为Leader。
- 3、其他步骤和初始化启动的时候一样。

## 3、搭建过程
> 1、将安装包上传到3台服务器上。

> 2、修改配置
```shell
# Leader和Follower每隔 2000ms 就会发送一个心跳，默认是 3000ms
tickTime=2000

# Leader服务器等待Follower启动并完整数据同步的时间，默认是10。当超过 10*tickTime 后，Leader还没有收到Follower的返回信息，表名这个Follower连接或同步失败。
initLimit=10

# Leader服务器和Follower服务器之间进行心跳检测的最大延时时间，默认值是5，最长不能超过5*tickTime。
syncLimit=5

# 存储数据结构的快照，便于快速恢复。
dataDir=/zookeeper/data

# 日志存放的目录
dataLogDir=/zookeeper/log

# zookeeper暴露的端口号
clientPort=2181

# server.1 这个里面的1是服务器的标识，可以是任意数字，标识是第几个服务器的节点，这个标识要写在dataDir目录下面的myid文件里
# 指定集群中通讯端口和选举端口
server.1=woniu01:2888:3888
server.2=woniu02:2888:3888
server.3=woniu03:2888:3888
```

> 3、创建文件夹
```shell
  mkdir /zookeeper/data
  mkdir /zookeeper/log
```

> 4、创建并写入节点到`myid`文件里
```shell
# woniu01主机，这里的“1”代表的是“server.1”中的“1”
echo "1" > /zookeeper/data/myid

# woniu02主机，这里的“2”代表的是“server.2”中的“2”
echo "2" > /zookeeper/data/myid

# woniu03主机，这里的“3”代表的是“server.3”中的“3”
```

> 5、分别去三台机器执行命令
```shell
  zkServer.sh start
```

<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。
