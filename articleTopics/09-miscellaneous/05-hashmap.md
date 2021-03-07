![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/04-arraylistarraylist.png)

# 目录-TODO
- 变量声明和构造器
- 数据结构
- put方法

## 1、变量声明和构造器
```java
public class HashMap<K,V> extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable {

    private static final long serialVersionUID = 362498820763181265L;
    
    //默认初始容量是16，必须是2的次幂
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16

    //最大的容量，如果隐士的指定更高的值，则使用两个带参数的构造函数组成。必须是 two <= 1<<30 次幂。
    static final int MAXIMUM_CAPACITY = 1 << 30;

    // 未指定负载因子时使用默认的负载因子 0.75
    static final float DEFAULT_LOAD_FACTOR = 0.75f;

    //当链表的值超过8会转红黑树
    static final int TREEIFY_THRESHOLD = 8;

    //当链表的值小于6会从红黑树转回链表
    static final int UNTREEIFY_THRESHOLD = 6;

    //转换为红黑树对应数组长度最小值
    static final int MIN_TREEIFY_CAPACITY = 64;

    static class Node<K,V> implements Map.Entry<K,V> {
        //根据key计算出来的hash值
        final int hash; 
        //key值
        final K key;
        //具体的值
        V value;
        //链表中下一个元素
        Node<K,V> next;
        Node(int hash, K key, V value, Node<K,V> next) {
            this.hash = hash;
            this.key = key;
            this.value = value;
            this.next = next;
        }
    }
    
    //构造器
    public HashMap() {
        this.loadFactor = DEFAULT_LOAD_FACTOR;
    }
    
    public HashMap(int initialCapacity) {
        this(initialCapacity, DEFAULT_LOAD_FACTOR);
    }

    
    public HashMap(int initialCapacity, float loadFactor) {
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " +
                                               loadFactor);
        this.loadFactor = loadFactor;
        this.threshold = tableSizeFor(initialCapacity);
    }
    
    public HashMap(Map<? extends K, ? extends V> m) {
        this.loadFactor = DEFAULT_LOAD_FACTOR;
        putMapEntries(m, false);
    }
```

## 2、JDK1.8数据结构
`数组:` 在内存中开辟的空间是连续的，占用内存大，所以空间复杂度大。数组中查询快，增删慢。  
`链表:` 存储区间离散，占用内存比较宽松，所以空间复杂度小。链表查询慢，增删慢。  
`HashMap：`满足数据的查找方便，同时不占用太多的内存空间。采用`Node`数组来存储key-value键值对，每一个键值对组成`Node`实体，`Node`类实际上是一个指针向下的单向链表结构。   
`红黑树：` 当数组的容量长度大于64并且链表长度大于8的时候链表数据结构会变成红黑树。`当链表的长度小于6会从红黑树转回链表。`因为防止在添加和删除元素的时候一直在长度8来回变，所以变成红黑树的机制和转回链表的机制定义的变量值分别为`8和6`。
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/05-hashmaphashmapadd.png)
`数组添加元素原理:` 从上面的图中可以看出，数组默认的大小是16，在数组上存储元素的原理是，通过取模的方式，将元素添加到指定的位置。通过上图我们可以看出来。   
`链表添加元素原理:` 因为在取模的时候会出现hash冲突，当出现hash冲突的时候，会出现链表。从上图可以看出。   
`红黑树添加元素原理：` 红黑树是基于二分查找树增强的，存在一个顶级节点，顶级节点左边的数据比顶级节点的数据小，顶级节点右边的数据要比顶级节点大，树通过左旋和右旋和变色来保持树的平衡。

## 3、put方法
```java
   public V put(K key, V value) {
         //调用putVal()方法
        return putVal(hash(key), key, value, false, true);
   }
    
    final V putVal(int hash, K key, V value, boolean onlyIfAbsent, boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        // 判断 table 是否初始化，否则初始化操作
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        // 计算存储的索引位置，如果没有元素，直接赋值
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e; K k;
            //节点如果已经存在，执行赋值操作。
            if (p.hash == hash && ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            //判断是否是红黑树
            else if (p instanceof TreeNode)
                //红黑树操作
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                //链表
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        //链表长度为8，将链表转化为红黑树存储
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    //如果key存在，直接覆盖。
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        //记录修改次数
        ++modCount;
        //判断是否需要扩容
        if (++size > threshold)
            resize();
        //空操作
        afterNodeInsertion(evict);
        return null;
    }
```
> 1、resize()
```java
// 扩容兼初始化
	final Node<K, V>[] resize() {
		Node<K, V>[] oldTab = table;
		int oldCap = (oldTab == null) ? 0 : oldTab.length;// 数组长度
		int oldThr = threshold;// 临界值
		int newCap, newThr = 0;
    
    //老的列表中有值
		if (oldCap > 0) {
		  //已经超过最大限制不在扩容，直接返回。MAXIMUM_CAPACITY = 1 << 30;
			if (oldCap >= MAXIMUM_CAPACITY) {
				threshold = Integer.MAX_VALUE;
				return oldTab;
       }
       
       // 新数组的长度扩展的是原来数组的2倍。
       else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY && oldCap >= DEFAULT_INITIAL_CAPACITY) {
				newThr = oldThr << 1;
			}
      
    // 如果没有指定initialCapacity, 则不会给threshold赋值, 该值被初始化为0
    // 如果指定了initialCapacity, 该值被初始化成大于initialCapacity的最小的2的次幂
    
    // 这里是指, 如果构造时指定了initialCapacity, 则用threshold作为table的实际大小
		} else if (oldThr > 0) {
			newCap = oldThr;
		} else {
			// 在默认无参数初始化会有这种情况
			newCap = DEFAULT_INITIAL_CAPACITY;// 16
			newThr = (int) (DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);// 0.75*16=12
		}
		if (newThr == 0) {
			// 如果新 的容量 ==0
			float ft = (float) newCap * loadFactor;// loadFactor 哈希加载因子 默认0.75,可在初始化时传入,16*0.75=12 可以放12个键值对
			newThr = (newCap < MAXIMUM_CAPACITY && ft < (float) MAXIMUM_CAPACITY ? (int) ft : Integer.MAX_VALUE);
		}
		threshold = newThr;// 将临界值设置为新临界值
		@SuppressWarnings({ "rawtypes", "unchecked" })
		// 扩容
		Node<K, V>[] newTab = (Node<K, V>[]) new Node[newCap];
		table = newTab;
		// 如果原来的table有数据，则将数据复制到新的table中
		if (oldTab != null) {
			// 根据容量进行循环整个数组，将非空元素进行复制
			for (int j = 0; j < oldCap; ++j) {
				Node<K, V> e;
				// 获取数组的第j个元素
				if ((e = oldTab[j]) != null) {
					oldTab[j] = null;
					// 如果链表只有一个，则进行直接赋值
					if (e.next == null)
						// e.hash & (newCap - 1) 确定元素存放位置
						newTab[e.hash & (newCap - 1)] = e;
					//  此处省略红黑树
					else {
						// 进行链表复制
						// 方法比较特殊： 它并没有重新计算元素在数组中的位置
						// 而是采用了 原始位置加原数组长度的方法计算得到位置
						Node<K, V> loHead = null, loTail = null;
						Node<K, V> hiHead = null, hiTail = null;
						Node<K, V> next;
						do {
							/*********************************************/
							/**
							 * 注: e本身就是一个链表的节点，它有 自身的值和next(链表的值)，但是因为next值对节点扩容没有帮助，
							 * 所有在下面讨论中，我近似认为 e是一个只有自身值，而没有next值的元素。
							 */
							/*********************************************/
							next = e.next;
							// 注意：不是(e.hash & (oldCap-1));而是(e.hash & oldCap)

							// (e.hash & oldCap) 得到的是 元素的在数组中的位置是否需要移动,示例如下
							// 示例1：
							// e.hash=10 0000 1010
							// oldCap=16 0001 0000
							//	 &   =0	 0000 0000       比较高位的第一位 0
							//结论：元素位置在扩容后数组中的位置没有发生改变
							
							// 示例2：
							// e.hash=17 0001 0001
							// oldCap=16 0001 0000
							//	 &   =1	 0001 0000      比较高位的第一位   1
							//结论：元素位置在扩容后数组中的位置发生了改变，新的下标位置是原下标位置+原数组长度
							
							// (e.hash & (oldCap-1)) 得到的是下标位置,示例如下
							//   e.hash=10 0000 1010
							// oldCap-1=15 0000 1111
							//      &  =10 0000 1010
								
							//   e.hash=17 0001 0001
							// oldCap-1=15 0000 1111
							//      &  =1  0000 0001
							
							//新下标位置
							//   e.hash=17 0001 0001
							// newCap-1=31 0001 1111    newCap=32
							//      &  =17 0001 0001    1+oldCap = 1+16
							
							//元素在重新计算hash之后，因为n变为2倍，那么n-1的mask范围在高位多1bit(红色)，因此新的index就会发生这样的变化：
							//参考博文：[Java8的HashMap详解](https://blog.csdn.net/login_sonata/article/details/76598675)  
							// 0000 0001->0001 0001

							if ((e.hash & oldCap) == 0) {
								// 如果原元素位置没有发生变化
								if (loTail == null)
									loHead = e;// 确定首元素
								// 第一次进入时	  e   -> aa  ; loHead-> aa
								else
									loTail.next = e;
								//第二次进入时		loTail-> aa  ;    e  -> bb ;  loTail.next -> bb;而loHead和loTail是指向同一块内存的，所以loHead.next 地址为 bb  
								//第三次进入时		loTail-> bb  ;    e  -> cc ;  loTail.next 地址为 cc;loHead.next.next = cc
								loTail = e;
								// 第一次进入时   	  e   -> aa  ; loTail-> aa loTail指向了和  loHead相同的内存空间
								// 第二次进入时               e   -> bb  ; loTail-> bb loTail指向了和  loTail.next（loHead.next）相同的内存空间   loTail=loTail.next
								// 第三次进入时               e   -> cc  ; loTail-> cc loTail指向了和  loTail.next(loHead.next.next)相同的内存
							} else {
								//与上面同理
								
								if (hiTail == null)
									hiHead = e;
								else
									hiTail.next = e;
								hiTail = e;
							}
						} while ((e = next) != null);//这一块就是 旧链表迁移新链表
						//总结：1.8中 旧链表迁移新链表    链表元素相对位置没有变化; 实际是对对象的内存地址进行操作 
						//在1.7中  旧链表迁移新链表        如果在新表的数组索引位置相同，则链表元素会倒置
						if (loTail != null) {
							loTail.next = null;// 将链表的尾节点 的next 设置为空
							newTab[j] = loHead;
						}
						if (hiTail != null) {
							hiTail.next = null;// 将链表的尾节点 的next 设置为空
							newTab[j + oldCap] = hiHead;
						}
					}
				}
			}
		}
		return newTab;
	}

```
- resize链表拆分
```java
Node<K,V> loHead = null, loTail = null;
Node<K,V> hiHead = null, hiTail = null;
Node<K,V> next;
do {
    next = e.next;
    if ((e.hash & oldCap) == 0) {
        if (loTail == null)
            loHead = e;
        else
            loTail.next = e;
        loTail = e;
    }
    else {
        if (hiTail == null)
            hiHead = e;
        else
            hiTail.next = e;
        hiTail = e;
    }
} while ((e = next) != null);
if (loTail != null) {
    loTail.next = null;
    newTab[j] = loHead;
}
if (hiTail != null) {
    hiTail.next = null;
    newTab[j + oldCap] = hiHead;
}
```
>> 第一段
>> ```java
>>   Node<K,V> loHead = null, loTail = null;
>>   Node<K,V> hiHead = null, hiTail = null;
>> ```
>>  定义了两个链表，称为lo链表和hi链表。loHead 和 loTail 分别指向 lo链表
>>  的头节点和尾节点。hiHead 和 hiTail 分别指向 hi链表的头节点和尾节点。
>> 
>> 第二段
>> ```java
>> do {
>>     next = e.next;
>>     if ((e.hash & oldCap) == 0) {
>>         if (loTail == null)
>>             loHead = e;
>>         else
>>             loTail.next = e;
>>         loTail = e;
>>     } else {
>>       if (hiTail == null)
>>           hiHead = e;
>>       else
>>           hiTail.next = e;
>>       hiTail = e;
>>     }
>> } while ((e = next) != null);
>> 
>> ```
>>  提出核心代码
>>  ```java
>>  // 插入lo
>>  if (loTail == null)
>>       loHead = e;
>>  else
>>      loTail.next = e;
>>  loTail = e;
>>  
>>  // 插入hi
>>  if (hiTail == null)
>>      hiHead = e;
>>  else
>>      hiTail.next = e;
>>  hiTail = e;
>>  ```
>>  上面是循环是按照顺序遍历集合中单个节点，我们首先准备了两个链表 lo 和 hi, 然后我们顺序遍历该存储桶上的链表的每个节点, 如果 (e.hash & oldCap) ==   0, 我们就将节点放入lo链表, 否则, 放入hi链表。
>> 第三段
>> ```java
>>    if (loTail != null) {
>>      loTail.next = null;
>>      newTab[j] = loHead;
>>    }
>>    if (hiTail != null) {
>>      hiTail.next = null;
>>      newTab[j + oldCap] = hiHead;
>>    }
>> ```
>> 如果lo链表非空, 我们就把整个lo链表放到新table的j位置上
>> 如果hi链表非空, 我们就把整个hi链表放到新table的j+oldCap位置上
>> ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/articleTopics/09-miscellaneous/05-hashmaphashmapresize01.png)

## 总结
Hashmap底层的数据结构是数组，因为数组查询快增删慢。又因为在存储数据时会有hash冲突，所以出现了链表。为了解决hash冲突。为了解决链表超长导致查询效率变低，所以出现了红黑树。

先判断hash值在判断equls，因为hash值不相等，对象一定不相等，对象不相等哈希值可能相等。

## TODO
数组扩展的时候为什么找到大于2的次幂方数？
为什么hashcode右移动和异或运算？

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一起快乐的学习。希望与您在网络的世界上会面。
