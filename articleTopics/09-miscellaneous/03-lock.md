![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/03-locklock.png)

# 目录
- 非公平锁
- 公平锁
- 读锁
- 写锁


## 1、非公平锁
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/03-lockunfairlock.png)
- 首先：线程1通过`CAS`获取锁成功（设置值为1）。
- 其次：线程2尝试通过`CAS`获取锁（设置值为1），但是获取锁失败。失败之后线程2会查看是不是自己加过锁，发现没有。加锁失败之后，就会进入等待队列中等待被唤醒。
- 再则：线程1执行完成之后，释放锁，并唤醒线程2，但是线程3，突然通过`CAS`获取锁（设置值为1），而且获取锁成功了。
- 最后：线程2进行获取锁的时候，发现锁已经被其他线程获取过了，又会继续进入等待队列继续等待。

## 2、公平锁
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/03-lockfairlock.png)
- 首先：线程1通过`CAS`获取锁成功（设置值为1）。
- 其次：线程2尝试通过`CAS`获取锁（设置值为1），但是获取锁失败。失败之后线程2会查看是不是自己加过锁，发现没有。加锁失败之后，就会进入等待队列中等待被唤醒。
- 再则：线程1执行完成之后，释放锁，并唤醒线程2，这个时候线程2通过`CAS`获取锁（设置值为1），设置成功。
- 最后：如果线程3进来，先查看等待队列中是否有等待获取锁的线程，如果有自己就加入在队列的后面。


## 3、读锁
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/03-lockread.png)
- 有一个线程加了读锁，其他线程也可以加读锁。
- 有线程加读锁，就不能加写锁了。

## 4、写锁
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/03-lockwritelock.png)
- 有一个线程加了写锁，其他线程不能加写锁。因为有线程要写共享数据。
- 有一个线程加了写锁，其他线程不能加读锁。

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一起快乐的学习。希望与您在网络的世界上会面。


