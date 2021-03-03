![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/01-miscellaneous/01-javavolatilevolatile.png)

# 目录
- 内存模型
- 并发编程中三个概念
- java内存模型
- Volatile 介绍
- 可见性
- 可见性的保证
- 原理和实现机制

## 1、内存模型
在计算机在执行程序时，每条指令都是在CPU中执行的，而执行指令过程中，就会涉及数据的读取和写入。由于程序运行过程中的临时数据是存放在主存当中的。由于CPU执行速度很快，而从内存读取数据和向内存写入数据的过程跟CPU执行指令的速度比起来要慢的多，因此如果任何时候对数据的操作都要通过和内存的交互来进行，会降低执行执行的速度，因此在CPU中就有了`高速缓存`。

## 2、并发编程中三个概念
> 1、原子性

一个操作要么或者多个操作，要么全部执行，要么全部不执行。

> 2、可见性

可见性是当多线程访问同一个变量时，一个线程修改了这个变量的值，其他线程能够立即看到修改的值。

> 3、有序性

程序执行的顺序按照代码先后顺序执行。

## 3、java内存模型
> 1、原子性

javan内存模型中只保证基本读取和赋值是原子性操作，如果想要实现大范围操作的原子性，可以通过`synchronized`和`Lock`来实现。因为`synchronized`和`Lock`能够保证任一时刻只有一个线程执行该代码块，所以就不存在原子性问题存在。

> 2、可见性

java提供`volatile`关键字保证可见性。

> 3、有序性

在java内存模型中，允许编译器和处理器对指令进行重排序，但是重排序不会影响到单线程程序的执行，却会影响多程序并发执行的正确性。  
java中`volatile`关键字和`synchronized`和`Lock`都能保证有序性。

## 4、Volatile 介绍
Java `volatile` 关键字用于将 Java 变量标记为`存储在主内存中`。这意味着每次读取变量都是从计算机的主内存中读取，而不是从CPU缓存中读取，并且对 `volatile` 标识的变量每次都将写入主内存中，而不仅仅写入到缓存中。

## 5、可见性
在多线程应用程序中，线程对变量的操作，出于性能方面的考虑，每个线程在对其进行处理时都将主存储器中的变量复制到属于自己的线程的缓存中。
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/01-miscellaneous/01-javavolatilevariable%20variability.png)

在操作变量时，无法保证虚拟机何时将数据从主存储器读取到CPU高速缓存中，或者何时将数据从高速缓存写入主存储器中。 

```java
public Demo {
    private int count = 0;
}
```
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/01-miscellaneous/01-javavolatilevariable%20variability%20example.png)
当程序运行时，线程1和线程2会将count加载到自己的高速缓冲区中，count的值初始为0，当线程1对count操作之后变成1，如果变量没有被`volatile`修饰时，修改后的值不会被重新写入主内存中。这样线程1和线程2中的值是不同的。  
由于线程尚未看到变量的最新值而导致该变量尚未被另一个线程写回到主内存中，被称为`可见性`问题。一个线程的更新对其他线程不可见。 

## 6、可见性的保证
- 被volatile修饰的变量，如果线程A写入值，并且线程B随后读取相同变量，则在写入volatile变量之前线程A可见的所有变量在读取volatile变量后也将对Thread B可见。

- 如果线程A读取了一个volatile变量，则读取该volatile变量时线程A可见的所有变量都会从主内存中重新读取。

## 7、原理和实现机制
观察加入volatile关键字和没有加入volatile关键字时所生成的汇编代码发现，加入volatile关键字时，会多出一个lock前缀指令。
这个前缀相当于一个屏障，屏障有3个功能：

- 确保指令重排序时不会把其后面的指令排到内存屏障中，也不会把前面的指令排到内存屏障后面；就是执行到内存屏障这句指令时，在他前面的操作已经全部完成。
- 他会强制将对缓存的修改操作立即写入主存中。
- 如果是写操作，他会导致其他CPU对应的缓存行无效。

<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。
