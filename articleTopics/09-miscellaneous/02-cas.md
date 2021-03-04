![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/02-cascas.png)

# 目录
- CAS
- 问题场景
- 解决方案
- Java中atomic
- 强大的LongAdder
- LongAdder原理

## 1、CAS
`CAS（Compare and swap）`比较和替换是设计并发算法时用到的一种技术。简单来说，比较和替换是使用一个期望值和一个变量的当前值进行比较，如果当前变量的值和我们期望的值相等，就使用一个新值来替换当前变量的值。

## 2、问题场景
```java
public class Demo{
  private int count = 0;
  // 多个线程同时对count操作： count++
}
```
如果在单线程情况下，这种操作是没问题的。如果是在多线程的情况下会出现问题。最后导致结果的不准确性。

## 3、解决方案
> 1、synchronized

```java
  public class Demo{
    private int count = 0;
    
    public synchronized void increment() {
        count++;
    }
    
    //多个线程同时调用方法：increment()
  }
```
这个时候，代码就是线程安全的了，因为加入了`synchronized`,也就是让每个线程进入`increment()`方法之前先尝试加锁，同一个时间只有一个线程能加锁，其他线程等待获取锁。

## 4、java中atomic
在jdk下有一个`java.util.concurrent.atomic`包，让我们学习一下。只简单介绍几个类，其他的类似。

> 1、`java.util.concurrent.atomic`中的类
- AtomicBoolean
- AtomicInteger
- AtomicIntegerArray
- AtomicIntegerFieldUpdater
- AtomicLong
- AtomicLongArray
- AtomicLongFieldUpdater
- AtomicMarkableReference
- AtomicReference
- AtomicReferenceArray
- AtomicReferenceFieldUpdater
- AtomicStampedReference
- LongAdder

> 2、AtomicBoolean
```java
  public class TestAtomicBoolean {

    public static void main(String[] args) {
        AtomicBoolean  atomicBoolean = new AtomicBoolean();
        
        //默认值是： false；这里设置值是true。
        atomicBoolean.set(true);

        //获取值
        boolean b = atomicBoolean.get();
        System.out.println(b);

        //设置值：arg1: 预期值 ； arg2: 修改值
        //如果预期值不一致，就会返回false,否则返回true。
        boolean b1 = atomicBoolean.compareAndSet(false, true);
        System.out.println(b1);

        boolean b2 = atomicBoolean.get();
        System.out.println(b2);
    }
}
//执行结果：
true
false
true
```

> 3、AtomicInteger
```java
public class TestAtomicInteger {
    public static void main(String[] args) {
        //设置初始值
        AtomicInteger atomicInteger = new AtomicInteger(10);

        atomicInteger.decrementAndGet(); //自减1
        atomicInteger.incrementAndGet(); //自增1
        atomicInteger.get();             //获取值
    }

}
```

> 4、AtomicIntegerArray
- 定义给定长度的容器和获取容器中元素的个数
```java
public class TestAtomicIntegerArray {
    public static void main(String[] args) {
        //设置给定长度的容器，默认值都是0。
        AtomicIntegerArray atomicIntegerArray = new AtomicIntegerArray(10);
        for (int i = 0; i < atomicIntegerArray.length(); i++) {
            System.out.println(atomicIntegerArray.get(i));
        }
    }
}
```
- 其他操作
```java
    @Test
    public void function02() {
        //设置给定长度的容器，默认值都是0。
        AtomicIntegerArray atomicIntegerArray = new AtomicIntegerArray(10);
        System.out.println("索引1位置的元素 ：" + atomicIntegerArray.get(1)); //获取指定索引的元素

        //arg1：索引位置
        //arg2：预期值
        //arg3: 修改的值
        //返回值：true 或 false
        //如果arg2的预期的值和实际索引位置上元素的值相等就会返回true。
        System.out.println(atomicIntegerArray.compareAndSet(0, 2, 9)); //false
        System.out.println(atomicIntegerArray.compareAndSet(0, 0, 9)); //true
        System.out.println("索引0位置的元素 ：" + atomicIntegerArray.get(0));

        //指定索引位置的上元素自增1
        System.out.println(atomicIntegerArray.incrementAndGet(0));

        //指定索引位置的上元素自减1
        System.out.println(atomicIntegerArray.decrementAndGet(0));
    }
```

## 5、 强大的LongAdder
```java
public class TestLongAdder {
    public static void main(String[] args){
        testAtomicLongVSLongAdder(1, 10000000);
        testAtomicLongVSLongAdder(10, 10000000);
        testAtomicLongVSLongAdder(20, 10000000);
        testAtomicLongVSLongAdder(40, 10000000);
        testAtomicLongVSLongAdder(80, 10000000);
    }

    static void testAtomicLongVSLongAdder(final int threadCount, final int times){
        try {
            System.out.println("threadCount：" + threadCount + ", times：" + times);
            long start = System.currentTimeMillis();
            testLongAdder(threadCount, times);
            System.out.println("LongAdder elapse：" + (System.currentTimeMillis() - start) + "ms");

            long start2 = System.currentTimeMillis();
            testAtomicLong(threadCount, times);
            System.out.println("AtomicLong elapse：" + (System.currentTimeMillis() - start2) + "ms");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    static void testAtomicLong(final int threadCount, final int times) throws InterruptedException {
        AtomicLong atomicLong = new AtomicLong();
        List<Thread> list = new ArrayList<>();
        for (int i=0;i<threadCount;i++){
            list.add(new Thread(() -> {
                for (int j = 0; j<times; j++){
                    atomicLong.incrementAndGet();
                }
            }));
        }

        for (Thread thread : list){
            thread.start();
        }

        for (Thread thread : list){
            thread.join();
        }
    }

    static void testLongAdder(final int threadCount, final int times) throws InterruptedException {
        LongAdder longAdder = new LongAdder();
        List<Thread> list = new ArrayList<>();
        for (int i=0;i<threadCount;i++){
            list.add(new Thread(() -> {
                for (int j = 0; j<times; j++){
                    longAdder.add(1);
                }
            }));
        }

        for (Thread thread : list){
            thread.start();
        }

        for (Thread thread : list){
            thread.join();
        }
    }
}
```

## 6、LongAdder原理
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/02-casLongAdder.png)

LongAdder的基本思路就是分散热点，将value值分散到一个数组中，不同线程会命中到数组的不同槽中，各个线程只对自己槽中的那个值进行CAS操作，

这样热点就被分散了，冲突的概率就小很多。如果要获取真正的long值，只要将各个槽中的变量值累加返回。

LongAdder继承自Striped64抽象类，Striped64中定义了Cell内部类和各重要属性。

<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。


