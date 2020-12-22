# 简介和应用场景

- 概要：
    - 介绍：
        - Redis支持五种数据类型：string（字符串）、hash（哈希）、list（列表）、set（集合）、zset（有序集合）。
    - 分类：
        - String（字符串）：
            - 定义：
                - string 是 redis 最基本的类型，一个 key 对应一个 value。string 类型是二进制安全的。因为 string 底层的实现是简单动态字符串 sds,是可以修改字符串。
            - 应用场景：
                - 1.单值缓存。
                - 2.对象缓存。
                - 3.分布式锁。
                - 4.常规计数。
                    - 粉丝数量、评论数量。
                - 5.WEB集群的session + redis实现 session 共享。
                - 6.分布式系统全局序列号。
        - Hash（哈希）：
            - 定义：
                - 是一个键值对集合。他相当于java中的双重map。<key,<filed,value>>
            - 应用场景： 
                - 购物车。
        - List（列表）：
            - 定义：
                - 列表是简单的字符串列表，按照插入顺序排序，可以添加一个元素在列表的头部或者尾部。
            - 应用场景：
                - 常用的数据结构。
                    - Stack（栈）= LPUSH + LPOP -> FILO //先进后出
                    - Queue（队列）= LPUSH + RPOP       //先进先出
                    - Blocking MQ（阻塞队列）= LPUSH + BRPOP //消息队列
                - 微博和微信公众号消息流。
        - Set（集合）：
            - 定义：
                - set是 string 类型的无序集合。
            - 应用场景：
                - 微信抽奖小程序。
                - 微信微博点赞、收藏、标签
                - 关注模型，就是可能认识的人的关系。
        - Zset（有序集合）：
            - 定义：
                - zset和set一样也是string类型元素的集合，且不允许重复的成员。不同的是每个元素都会关联一个dobule类型的分数，redis正是通过分数为集合成员进行从小到大的排序，zset的成员是唯一的但是分数可以重复。
            - 场景应用：
                - 
- 语法：
    ```shell
        string
            单值缓存:
                SET key value
                GET key
            对象缓存：
                1. SET user:1 value(json格式数据)
                2. MSET user:1:name tsingli user:1:balance 1888
                   MGET user:1:name user:1:balance
            分布式锁：
                线程1： SETNX product:1001 true //返回1代表获取锁成功
                线程2： SETNX product:1001 true //返回0代表获取锁失败
                。。。执行业务操作
                DEL product:1001               //执行完业务释放锁

                SET product:1001 true ex 10 nx //防止程序意外终止导致死锁
                案例：
                    减库存的方法：
                        {
                            SETNX product:1001 true
                                1.查询商品1001的库存
                                2.减库存
                                3.重新把减完剩余的库存更新回数据库
                            DEL product:1001
                        }
                    SETNX 如果插入的key一样不会对数据有任何操作，如果第二次对库存再进行减对的话就返回错误。
            常规计数器：
                INCR article:readcount:{文章id}
                GET  article:readcount:{文章id}
            分布式系统全局序列号：
                INCRBY orderid 1000  //redis批量生成序列号提升性能
        hash
            购物车：
                说明：
                    用户id为1001，商品的编码是10088
                案例：
                    用户id为key
                    商品id为field
                    商品数量为value
                购物车操作：
                    添加商品：
                        hset cart:1001 10088 1
                    增加数量：
                        hincrby cart:1001 10088 1
                    商品总数：
                        hlen cart:1001
                    删除商品：
                        hdel cart:1001 10088
                    获取购物车所有商品：
                        hgetall cart:1001
        list
            微博和微信公众号消息流：
                mactalk发微博，消息id为10018
                    LPUSH msg:111111 10018
                备胎说车发微博，消息id为10086
                    LPUSH msg:111111 10086
                查看最新微博消息
                    LRANGE msg:11111 0 5 //0至5的微博消息。
        set
            微信抽奖小程序:
                点击参与抽奖加入集合
                    SADD key {userId}
                查看参与抽奖的所有用户
                    SMEMBERS key
                抽取count名中奖者（1） // SRANDMEMBER不会将元素从集合中删除
                    SRANDMEMBER key [count] //抽取两名中奖者 SRANDMEMBER act:1008 2
                抽取count名中奖者（2） // SPOP会将元素从集合中删除
                    SPOP key 2
            微信微博点赞、收藏、标签：
                点赞
                    SADD like:{消息ID} {用户id}
                取消点赞
                    SREM like:{消息ID} {用户id}
                检查用户是否点过赞
                    SISMEMBER like:{消息ID} {用户id}
                获取点赞的用户列表
                    SMEMBERS like:{消息ID}
                获取点赞的用户树
                    SCARD like:{消息ID}
      
    ```
- 案例：
    ```java

    ```
