![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/04-arraylistarraylist.png)

# 目录
- ArrayList为什么不安全？
- 总结
- ArrayList怎么才能变成安全的集合呢？
- transient

## 1、ArrayList为什么不安全？
> 1、故事开头

我胆战心惊的来到面试现场，胆战心惊的等待着面试官提问问题。
>> `面试官：`你用过ArrayList吗？  
>> 青衣：用过。  
>> `面试官：`那你讲讲其中的原理吧。  
>> 巴拉巴拉青衣讲了一大堆。。。    
>> `面试官：`很好，那你可以说说ArrayList为什么不安全吗？  
>> 青衣：额，这个我不知道。   
>> `面试官：`额，那我们的面试就到这里吧，回去等通知。

> 2、基本变量的声明和构造器
```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable{

    private static final long serialVersionUID = 8683452581122892189L;

    //默认初始容量
    private static final int DEFAULT_CAPACITY = 10;

    //用于空实例的共享空数组实例
    private static final Object[] EMPTY_ELEMENTDATA = {};

    /**
     * 用于默认大小的空实例的共享空数组实例。
     * 我们将其与EMPTY_ELEMENTDATA区分开来，以了解添加第一个元素时扩容多少。
     * MARK:无参构造函数 使用该数组初始化 与EMPTY_ELEMENTDATA的区别主要是区分作用，用来减少空数组的存在，优化内存使用 1.8后的优化
     */
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

     /**
      * 存储集合元素的数组缓冲区，集合的容量是此数组的缓冲区的长度，添加第一个元素时用elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA， 我们会通过DEFAULT_CAPACITY扩展容量。
     */
    transient Object[] elementData; // non-private to simplify nested class access

    //集合的大小
    private int size;
  
   /**
    * 构造一个具有指定初始容量的空列表。
    */
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }

    // 构造一个初始容量为10的空列表
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }

    // 构造一个包含指定 collection 的元素的列表，这些元素是按照该 collection 的迭代器返回它们的顺序排列的。
    public ArrayList(Collection<? extends E> c) {
        Object[] a = c.toArray();
        if ((size = a.length) != 0) {
            if (c.getClass() == ArrayList.class) {
                elementData = a;
            } else {
                elementData = Arrays.copyOf(a, size, Object[].class);
            }
        } else {
            // replace with empty array.
            elementData = EMPTY_ELEMENTDATA;
        }
    }
}
```
总结：如果创建集合的时候，如果构造器中声明了一个具体的数字，集合底层就会初始化一个指定初始容量的`空数组`。如果创建集合的时候，构造器中如果没有填写数字，集合底层就会初始化一个默认大小为10的`数组`。

> 3、元素的添加
```java
    public boolean add(E e) {
        // 判断数组的容量是否足够，是否需要扩容。
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        // 将元素添加到指定的位置。
        elementData[size++] = e;
        return true;
    }
```
>> 问题1：
>> ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/04-arraylistarraylistadd.png)

>> 问题2：  
>> elementData[size++] = e，这一步不是原子操作，分为了两步。   
>> - elementData[size] = e;
>> - size = size + 1;
>> ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/04-arraylistarraylistadd01.png)

## 2、总结
导致ArrayList不安全的原因是上面两点：
- 当执行添加方法的时候，先判断容器是否可以存放数据，两条线程都判断容器可以存放数据，然后当其中一条线程设置完值之后，另一条线程再次设置值，发现容器长度不够。
- `elementData[size++] = e`这一步应为不是原子操作，所以在添加数据的时候会出现null。

## 3、ArrayList怎么才能变成安全的集合呢？
> 1、 Collections.synchronizedList()
```java
public static void main(String[] args) throws InterruptedException {
        List<String> list = Collections.synchronizedList(new ArrayList<>());
        for (int i = 1; i < 300; i++) {
            new Thread(()->{
                list.add("234343412333333333333333333333333333333");
                System.out.println(list);
            }).start();

        }
}
```

> 2、CopyOnWriteArrayList
```java
public class Test {

    public static void main(String[] args) throws InterruptedException {

        CopyOnWriteArrayList list1 = new CopyOnWriteArrayList();
        for (int i = 1; i < 300; i++) {
            new Thread(()->{
                list1.add("234343412333333333333333333333333333333");
                System.out.println(list1);
            }).start();

        }
    }

}
```

## 4、transient
ArrayList中`elementData`用`transient`修饰，但是被`transient`修饰的变量是不会被序列化的但是为什么集合又能序列化呢？
```java
private void writeObject(java.io.ObjectOutputStream s)
        throws java.io.IOException{
        // Write out element count, and any hidden stuff
        int expectedModCount = modCount;
        s.defaultWriteObject();

        // Write out size as capacity for behavioural compatibility with clone()
        s.writeInt(size);

        // Write out all elements in the proper order.
        for (int i=0; i<size; i++) {
            s.writeObject(elementData[i]);
        }

        if (modCount != expectedModCount) {
            throw new ConcurrentModificationException();
        }
    }
    
 private void readObject(java.io.ObjectInputStream s)
        throws java.io.IOException, ClassNotFoundException {
        elementData = EMPTY_ELEMENTDATA;

        // Read in size, and any hidden stuff
        s.defaultReadObject();

        // Read in capacity
        s.readInt(); // ignored

        if (size > 0) {
            // be like clone(), allocate array based upon size not capacity
            int capacity = calculateCapacity(elementData, size);
            SharedSecrets.getJavaOISAccess().checkArray(s, Object[].class, capacity);
            ensureCapacityInternal(size);

            Object[] a = elementData;
            // Read in all elements in the proper order.
            for (int i=0; i<size; i++) {
                a[i] = s.readObject();
            }
        }
    }
```

ArrayList在序列化的时候会调用writeObject，直接将size和element写入ObjectOutputStream；反序列化时调用readObject，从ObjectInputStream获取size和element，再恢复到elementData。为什么不直接用elementData来序列化，而采用上诉的方式来实现序列化呢？原因在于elementData是一个缓存数组，它通常会预留一些容量，等容量不足时再扩充容量，那么有些空间可能就没有实际存储元素，采用上诉的方式来实现序列化时，就可以保证只序列化实际存储的那些元素，而不是整个数组，从而节省空间和时间。

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一起快乐的学习。希望与您在网络的世界上会面。


