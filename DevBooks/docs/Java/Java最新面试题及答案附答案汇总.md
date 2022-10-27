# Java最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、js如何实现页面刷新呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#1js如何实现页面刷新呢)  


**1、** history.go(0)

**2、** location.reload()


### [2、什么是线程池？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#2什么是线程池)  


在一个应用程序中初始化一个线程集合，然后在需要执行新的任务时重用线程池中的线程，而不是创建一个新的线程。线程池中的每个线程都有被分配一个任务，一旦任务完成，线程就回到线程池中，等待下一次的任务分配


### [3、如何实现 Array 和 List 之间的转换？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#3如何实现-array-和-list-之间的转换)  


**1、** Array 转 List： Arrays、asList(array) ；

**2、** List 转 Array：List 的 toArray() 方法。


### [4、普通类和抽象类有哪些区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#4普通类和抽象类有哪些区别)  


普通类不能包含抽象方法，抽象类可以包含抽象方法。 抽象类不能直接实例化，普通类可以直接实例化。


### [5、为什么线程通信的方法wait(), notify()和notifyAll()被定义在Object 类里？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#5为什么线程通信的方法wait,-notify和notifyall被定义在object-类里)  


Java的每个对象中都有一个锁(monitor，也可以成为监视器) 并且wait()，notify()等方法用于等待对象的锁或者通知其他线程对象的监视器可用。在Java的线程中并没有可供任何对象使用的锁和同步器。这就是为什么这些方法是Object类的一部分，这样Java的每一个类都有用于线程间通信的基本方法。


### [6、遍历一个 List 有哪些不同的方式？每种方法的实现原理是什么？Java 中 List 遍历的最佳实践是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#6遍历一个-list-有哪些不同的方式每种方法的实现原理是什么java-中-list-遍历的最佳实践是什么)  


**遍历方式有以下几种：**

**1、** for 循环遍历，基于计数器。在集合外部维护一个计数器，然后依次读取每一个位置的元素，当读取到最后一个元素后停止。

**2、** 迭代器遍历，Iterator。Iterator 是面向对象的一个设计模式，目的是屏蔽不同数据集合的特点，统一遍历集合的接口。Java 在 Collections 中支持了 Iterator 模式。

**3、** foreach 循环遍历。foreach 内部也是采用了 Iterator 的方式实现，使用时不需要显式声明 Iterator 或计数器。优点是代码简洁，不易出错；缺点是只能做简单的遍历，不能在遍历过程中操作数据集合，例如删除、替换。

**最佳实践：**

Java Collections 框架中提供了一个 RandomAccess 接口，用来标记 List 实现是否支持 Random Access。

**1、** 如果一个数据集合实现了该接口，就意味着它支持 Random Access，按位置读取元素的平均时间复杂度为 O(1)，如ArrayList。

**2、** 如果没有实现该接口，表示不支持 Random Access，如LinkedList。

**3、** 推荐的做法就是，支持 Random Access 的列表可用 for 循环遍历，否则建议用 Iterator 或 foreach 遍历。


### [7、String str="i"与 String str=new String("i")一样吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#7string-str="i"与-string-str=new-string"i"一样吗)  


不一样，因为内存的分配方式不一样。String str="i"的方式，java 虚拟机会将其分配到常量池中；而 String str=new String("i") 则会被分到堆内存中。


### [8、用过ConcurrentHashMap，讲一下他和HashTable的不同之处？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#8用过concurrenthashmap讲一下他和hashtable的不同之处)  


ConcurrentHashMap是Java5中支持高并发、高吞吐量的线程安全HashMap实现。它由Segment数组结构和HashEntry数组结构组成。Segment数组在ConcurrentHashMap里扮演锁的角色，HashEntry则用于存储键-值对数据。一个ConcurrentHashMap里包含一个Segment数组，Segment的结构和HashMap类似，是一种数组和链表结构；一个Segment里包含一个HashEntry数组，每个HashEntry是一个链表结构的元素；每个Segment守护着一个HashEntry数组里的元素，当对HashEntry数组的数据进行修改时，必须首先获得它对应的Segment锁。

**看不懂？？？很正常，我也看不懂**

**总结：**

**1、** HashTable就是实现了HashMap加上了synchronized，而ConcurrentHashMap底层采用分段的数组+链表实现，线程安全

**2、** ConcurrentHashMap通过把整个Map分为N个Segment，可以提供相同的线程安全，但是效率提升N倍，默认提升16倍。

**3、** 并且读操作不加锁，由于HashEntry的value变量是 volatile的，也能保证读取到最新的值。

**4、** Hashtable的synchronized是针对整张Hash表的，即每次锁住整张表让线程独占，ConcurrentHashMap允许多个修改操作并发进行，其关键在于使用了锁分离技术

**5、** 扩容：段内扩容（段内元素超过该段对应Entry数组长度的75%触发扩容，不会对整个Map进行扩容），插入前检测需不需要扩容，有效避免无效扩容


### [9、线程的基本状态以及状态之间的关系？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#9线程的基本状态以及状态之间的关系)  




![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/03/img_2.png#alt=img%5C_2.png)

> 说明：其中Running表示运行状态，Runnable表示就绪状态（万事俱备，只欠CPU），Blocked表示阻塞状态，阻塞状态又有多种情况，可能是因为调用wait()方法进入等待池，也可能是执行同步方法或同步代码块进入等锁池，或者是调用了sleep()方法或join()方法等待休眠或其他线程结束，或是因为发生了I/O中断。



### [10、线程池中 submit() 和 execute() 方法有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案附答案汇总.md#10线程池中-submit-和-execute-方法有什么区别)  


**相同点：**

相同点就是都可以开启线程执行池中的任务。

**不同点：**

**1、** 接收参数：execute()只能执行 Runnable 类型的任务。submit()可以执行 Runnable 和 Callable 类型的任务。

**2、** 返回值：submit()方法可以返回持有计算结果的 Future 对象，而execute()没有

**3、** 异常处理：submit()方便Exception处理


### 11、工厂模式分类
### 12、GC Roots 有哪些？
### 13、Static关键字有什么作用？
### 14、如何部署一个web项目？
### 15、Jsp由哪些内容组成？
### 16、为什么你应该在循环中检查等待条件?
### 17、重载和重写的区别
### 18、什么是Future？
### 19、请说明select * from tab的输出结果是什么?
### 20、JVM 提供的常用工具
### 21、CyclicBarrier和CountDownLatch的区别
### 22、Collection 和 Collections 有什么区别？
### 23、safepoint 是什么？
### 24、List、Map、Set三个接口存取元素时，各有什么特点？
### 25、什么是线程池（thread pool）？
### 26、什么是Executors框架？
### 27、Java中Synchronized关键字的使用？
### 28、对象的内存布局了解吗？
### 29、什么是链表
### 30、TCP 协议与 UDP 协议有什么区别？
### 31、代理模式应用场景
### 32、Super与this表示什么？
### 33、volatile 能使得一个非原子操作变成原子操作吗？
### 34、可以描述一下 class 文件的结构吗？
### 35、聚集索引与非聚集索引有什么区别？
### 36、JAVA为什么需要接口？
### 37、你知道哪些GC类型？
### 38、62、volatile 变量和 atomic 变量有什么不同？
### 39、HashSet如何检查重复？HashSet是如何保证数据不可重复的？
### 40、volatile有什么用？能否用一句话说明下volatile的应用场景？
### 41、异常的处理机制有几种？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




