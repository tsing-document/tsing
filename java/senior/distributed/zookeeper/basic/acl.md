![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/zookeeper/basic/java-senior-distriuted-zookeeper-%E5%9F%BA%E7%A1%80%E7%AF%87-ACL.png)

# 目录
- 概述
- ACL 构成方式
- 权限模式
- ACL 命令行
- 案例

## 1、概述    
>（1）ACL（权限控制表，Access Control List）可以针对节点设置相关读写等权限，保障数据安全性。 

>（2）zookeeper的权限控制是基于每个znode节点的，需要对每个节点设置权限。

>（3）每个znode支持设置多种全限控制方案和多个权限。

>（4）子节点不会继承父节点的权限，客户端无权访问某个节点，但可能可以访问他的子节点。

## 2、ACL 构成方式
格式：**[scheme:id:permissions]**  
说明：
- `scheme`: 代表权限的某种权限模式，权限模式的分类：world、auth、digest、ip、super。 这个地方确认一下新版本里面是否存在。
- `id`: 代表允许访问的用户。
- `permissions`: 权限组合字符串，由**cdrwa**组成。 c（创建权限）d（删除权限）r（读取权限）w（写入权限）a（管理权限）。


## 3、权限模式
| 模式    |  描述   |
| --- | --- |
| world    |  只有一个用户：anyone,代表登录zookeeper所有人（默认）   |
| ip    |  对客户端使用ip地址认证   |
| auth   |  使用已经添加认证的用户认证    |
| digest    |  使用 `用户名：密码` 方式认证   |
| super    |  一起填充啊！！哈哈   |

## 4、ACL 命令行
> 格式：`getAcl <path>`  
说明：获取某个节点的权限信息。


> 格式：`setAcl <path>  <acl>`  
说明：设置某个节点的权限信息。

> 格式：`addauth <scheme> <auth>`  
说明：添加认证用户，注册时输入明文密码，加密形式保护。


## 5、案例
> （1）world模式：
- 格式：`setAcl <path> <acl>`
```shell
    ## 查看节点信息
    [zk: localhost:2181(CONNECTED) 9] ls /
    [tsing, zookeeper]
    [zk: localhost:2181(CONNECTED) 10] ls /tsing
    [child, child11, child22]
    
    ## 查看节点权限
    [zk: localhost:2181(CONNECTED) 11] getAcl /tsing/child
    'world,'anyone: cdrwa
    
    ## 设置节点权限 world:anyone:drwa
    [zk: localhost:2181(CONNECTED) 12] setAcl /tsing/child world:anyone:drwa
    
    ## 查看节点权限
    [zk: localhost:2181(CONNECTED) 13] getAcl /tsing/child
    'world,'anyone: drwa
      
    ## 测试节点权限
    [zk: localhost:2181(CONNECTED) 14] create /tsing/child/subchild "subchild111"
    Authentication is not valid : /tsing/child/subchild

```

> （2）IP模式：
- 格式：`setAcl <path> ip:<ip>:<acl>`
```shell
    ## 查看节点信息
    [zk: localhost:2181(CONNECTED) 2] ls /tsing
    [child, child11, child22]
    
    ## 查看节点权限
    [zk: localhost:2181(CONNECTED) 4] getAcl /tsing/child11
    'world,'anyone
    : cdrwa
    
    ## 设置节点权限
    [zk: localhost:2181(CONNECTED) 5] setAcl /tsing/child11 ip:47.101.159.7:cdrwa
    
    ## 测试节点权限
    [zk: localhost:2181(CONNECTED) 6] getAcl /tsing/child11
    Authentication is not valid : /tsing/child11
    
    ## 测试其他节点权限
    [zk: localhost:2181(CONNECTED) 7] getAcl /tsing/child22
    'world,'anyone
    : cdrwa
```

> （3）auth 模式：   
- （1）先添加认证用户:
  - 格式：`addauth digest <user>:<acl>`

- （2）设置权限：
  - 格式：`setAcl <path> auth:<user>:<acl>`  
```shell
    ## 客户端1
    ### 添加用户
    [zk: localhost:2181(CONNECTED) 14] addauth digest  woniu:123456
    ### 设置权限
    [zk: localhost:2181(CONNECTED) 15] setAcl /tsing/child22 auth:woniu:cdrwa
    
    ### 查看acl
    [zk: localhost:2181(CONNECTED) 16] getAcl /tsing/child22
    'digest,'woniu:gf5TyYuxn0ddZm/UMG/QP9RcOFM=
    : cdrwa

    ### 因为当前会话已经添加用户，所有可以查看节点数据
    [zk: localhost:2181(CONNECTED) 17] get /tsing/child22
    child22
    
    ## 重新打开一个 客户端2
    ### 查看节点信息
    [zk: localhost:2181(CONNECTED) 3] ls /tsing/child22
    Authentication is not valid : /tsing/child22

    ### 将用户添加到当前会话
    [zk: localhost:2181(CONNECTED) 4] addauth digest woniu:123456

    ### 查看节点数据
    [zk: localhost:2181(CONNECTED) 6] get  /tsing/child22
    child22
```

> （4）digest 模式：
- 格式：`setAcl <path> digest:<user>:<password>:<acl>`
- 说明：密码要经过SHA1和BASE64处理的密文，用下面的命令在shell中执行：
- 将`<user>:<password>`替换成自己的。
```shell
  echo -n <user>:<password> | openssl dgst -binary -sha1 | openssl base64
```

```shell
  ## 加密密码
  [root@izuf6d2cbgi4jtuapl9yfnz ~]#  echo -n woniu:123456 | openssl dgst -binary -sha1 | openssl base64
  gf5TyYuxn0ddZm/UMG/QP9RcOFM=
  
  ## 设置权限
  setAcl /tsing/child33 digest:woniu:gf5TyYuxn0ddZm/UMG/QP9RcOFM=:cdrwa
  
  ## 客户端2
  [zk: localhost:2181(CONNECTED) 9] addauth digest woniu:123456

  [zk: localhost:2181(CONNECTED) 11] get  /tsing/child33
  child33
```

- （5）super 模式
- 和我一起填充内容啊！

<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。


