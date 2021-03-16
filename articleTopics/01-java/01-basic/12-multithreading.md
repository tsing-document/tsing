![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/01-java/01-basic/12-multithreadingcoverpicture.png)

# 目录
- 1、概述
- 2、进程和线程
- 3、创建线程的方式
- 4、线程的状态
- 5、线程池创建之Executors
- 6、自定义多线程

## 1、概述
`百度百科`中这样解释多线程：多线程（multithreading）：是指从软件或者硬件上实现多个线程并发执行的技术。具有多线程能力的计算机因有硬件支持而能够在同一时间执行多于一个线程，进而提升整体处理性能。具有这种能力的系统包括对称多处理机、多核心处理器以及芯片级多处理或同时多线程处理器。在一个程序中，这些独立运行的程序片段叫作`线程`（Thread），利用它编程的概念就叫作`多线程处理` 。

## 2、进程和线程
> 1、进程

`百度百科`中这样解释进程：进程（Process）是计算机中的程序关于某数据集合上的一次运行活动，是系统进行资源分配和调度的基本单位，是操作系统结构的基础。程序是指令、数据及其组织形式的描述，进程是程序的实体。  
比如运行的QQ、微信、浏览器等等。。。

> 2、线程

`百度百科`中这样解释线程：线程（thread）是操作系统能够进行运算调度的最小单位。一个进程中可以并发多个线程，每条线程并行执行不同的任务。  
比如看视频的时候可以看视频、听声音、看弹幕等等。。。

## 3、创建线程的方式
> 1、继承Thread
```java
package com.tsing.multithreading;

public class DemoThread extends Thread{

    @Override
    public void run() {
        System.out.println("线程的名称--》 " + Thread.currentThread().getName() +  "--》 我是run方法，正在执行！！！！");
    }

    public static void main(String[] args) {
        DemoThread demoThread = new DemoThread();
        demoThread.start();

        System.out.println("线程的名称--》 " + Thread.currentThread().getName() + "--》 我是main方法，正在执行！！！");
    }
}
```

> 2、实现Runable
```java
package com.tsing.multithreading;

public class DemoRunable implements Runnable{

    @Override
    public void run() {
        System.out.println("线程的名称--》 " + Thread.currentThread().getName() + "--》 我是Runable接口中的run()方法，正在执行！！！！");
    }

    public static void main(String[] args) {
        DemoRunable demoRunable = new DemoRunable();
        new Thread(demoRunable).start();

        System.out.println("线程的名称--》 " + Thread.currentThread().getName() + "--》 我是实现Runable接口的main方法，正在执行!!!");
    }
}
```

> 3、实现Callable
```java
package com.tsing.multithreading;

import java.util.concurrent.*;

public class DemoCallAble implements Callable<Boolean> {

    @Override
    public Boolean call() throws Exception {
        System.out.println("线程的名称--》 " + Thread.currentThread().getName() + "--》 我是Callable接口中的call()方法，正在执行！！！！");
        return true;
    }

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        DemoCallAble cd1 = new DemoCallAble();
        DemoCallAble cd2 = new DemoCallAble();
        DemoCallAble cd3 = new DemoCallAble();

        ExecutorService es = Executors.newFixedThreadPool(3);

        Future<Boolean> r1 = es.submit(cd1);
        Future<Boolean> r2 = es.submit(cd2);
        Future<Boolean> r3 = es.submit(cd3);

        Boolean b1 = r1.get();
        Boolean b2 = r2.get();
        Boolean b3 = r3.get();

        es.shutdown();

        System.out.println("线程的名称--》 " + Thread.currentThread().getName() + "--》 我是实现Callable接口中的main()方法，正在执行！！！！");
    }
}
```

## 4、线程的状态
> 1、线程的六种状态

![](https://img-blog.csdnimg.cn/20181120173640764.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BhbmdlMTk5MQ==,size_16,color_FFFFFF,t_70)

**线程有六中状态：** 初始状态、可运行状态、阻塞状态、等待状态、等待指定时间、终止状态。

> 2、线程状态之间的转化   

>> `1、初始状态（NEW）：`新建一个线程后，调用`start()`方法之前线程处于初始状态。

>> `2、运行状态（RUNNABLE-READY）：` 
>>> 1、就绪状态只是说你有资格运行，调用程序没有挑选到你，你就永远是就绪状态。  
>>> 2、调用线程的`start()`方法，此线程进入就绪状态。  
>>> 3、当前线程`sleep()`方法结束，其他线程`join()`结束，等待用户输入完毕，某个线程拿到对象锁，这些线程也将进入就绪状态。  
>>> 4、当前线程时间片用完了，调用当前线程的`yield()`方法，当前线程进入就绪状态。  
>>> 5、锁池里的线程拿到对象锁后，进入就绪状态。

>> `2、运行状态（RUNNABLE-RUNNING）：` 
线程调度程序从可运行池中选择一个线程作为当前线程时线程所处的状态。这也是线程进入运行状态的唯一一种方式。
 
>> `3、阻塞状态（BLOCKED）：`线程等待锁的状态。等待获取锁进入同步代码块/方法或者调用wait()方法后重新进入需要竞争锁。    

>> `4、等待状态（WAITING）：`一个线程在等待另一个线程执行动作时。调用下面的方法线程进入**等待状态**：Object.wait()、Object.join()、LockSupport.park()。处于该状态的线程是不会自动唤醒的，必须等待另一个线程调用notify()或notifyAll()方法才能唤醒。   

>> `5、等待指定时间（TIMED_WAITING）`：指定线程等待时间，等时间结束后自动唤醒并进入竞争锁的队列。调用以下方法进入等待指定时间。Thread.sleep、Object.wait with timeout、Thread.join with timeout、LockSupport.parkNanos、LockSupport.parkUntil。   

>> `6、终止状态（TERMINATED）：`线程执行完毕或者出现异常时。

## 5、线程池创建之Executors
以下三个方法都会调用下面的构造器：
```java
public ThreadPoolExecutor(int corePoolSize, //核心线程数
                          int maximumPoolSize, //非核心线程数
                          long keepAliveTime, //时间，指定当线程在多久时间没有被使用就去除掉。
                          TimeUnit unit,//时间单位
                          BlockingQueue<Runnable> workQueue,//队列
                          ThreadFactory threadFactory,//线程工厂
                          RejectedExecutionHandler handler //拒绝策略) {
       // 省略代码。。。                       
}
```

> 1、Executors.newFixedThreadPool(int nThreads); //慢

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/01-java/01-basic/12-multithreadingnewFixedThreadPool.png)


> 2、Executors.newCachedThreadPool(); //快

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/01-java/01-basic/12-multithreadingnewCachedThreadPool.png)


> 3、Executors.newSingleThreadExecutor(); //最慢

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/01-java/01-basic/12-multithreadingnewSingleThreadExecutor.png)

## 6、自定义多线程
> 1、ThreadPoolExecutor

```java
package com.tsing.multithreading;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

public class DemoExecutors {

    public static void main(String[] args) {
        ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(
                10, 20, 0L,
                TimeUnit.MILLISECONDS, new ArrayBlockingQueue<Runnable>(10));
        for (int i = 0; i < 100; i++) {
            threadPoolExecutor.execute(new MyThread());
        }
    }
}

class  MyThread implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName() + i);
        }
    }
}
```
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/01-java/01-basic/12-multithreadingThreadPoolExecutor.png)


<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一起快乐的学习。希望与您在网络的世界上会面。


