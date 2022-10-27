# Java面试题目大汇总，附参考答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、StringBuffer，Stringbuilder有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#1stringbufferstringbuilder有什么区别)  


StringBuffer与StringBuilder都继承了AbstractStringBulder类，而AbtractStringBuilder又实现了CharSequence接口，两个类都是用来进行字符串操作的。

在做字符串拼接修改删除替换时，效率比string更高。

StringBuffer是线程安全的，Stringbuilder是非线程安全的。所以Stringbuilder比stringbuffer效率更高，StringBuffer的方法大多都加了synchronized关键字


### [2、什么是分布式垃圾回收（DGC）？它是如何工作的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#2什么是分布式垃圾回收dgc它是如何工作的)  


DGC 叫做分布式垃圾回收。RMI 使用 DGC 来做自动垃圾回收。因为 RMI 包含了跨虚拟机的远程对象的引用，垃圾回收是很困难的。DGC 使用引用计数算法来给远程对象提供自动内存管理。


### [3、OSGI（ 动态模型系统）](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#3osgi-动态模型系统)  


OSGi(Open Service Gateway Initiative)，是面向 Java 的动态模型系统，是 Java 动态化模块化系统的一系列规范。


### [4、什么是方法的返回值？返回值在类的方法里的作用是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#4什么是方法的返回值返回值在类的方法里的作用是什么)  


方法的返回值是指我们获取到的某个方法体中的代码执行后产生的结果！（前提是该方法可能产生结果）。返回值的作用:接收出结果，使得它可以用于其他的操作！


### [5、什么是线程死锁](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#5什么是线程死锁)  


**1、** 死锁是指两个或两个以上的进程（线程）在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象，若无外力作用，它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁，这些永远在互相等待的进程（线程）称为死锁进程（线程）。

**2、** 多个线程同时被阻塞，它们中的一个或者全部都在等待某个资源被释放。由于线程被无限期地阻塞，因此程序不可能正常终止。

**3、** 如下图所示，线程 A 持有资源 2，线程 B 持有资源 1，他们同时都想申请对方的资源，所以这两个线程就会互相等待而进入死锁状态。

![87_1.png][87_1.png]


### [6、JVM中一次完整的GC流程是怎样的，对象如何晋升到老年代？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#6jvm中一次完整的gc流程是怎样的对象如何晋升到老年代)  


当 Eden 区的空间满了， Java虚拟机会触发一次 Minor GC，以收集新生代的垃圾，存活下来的对象，则会转移到 Survivor区。大对象（需要大量连续内存空间的Java对象，如那种很长的字符串）直接进入老年态；如果对象在Eden出生，并经过第一次Minor GC后仍然存活，并且被Survivor容纳的话，年龄设为1，每熬过一次Minor GC，年龄+1，若年龄超过一定限制（15），则被晋升到老年态。即长期存活的对象进入老年态。老年代满了而无法容纳更多的对象，Minor GC 之后通常就会进行Full GC，Full GC 清理整个内存堆 – 包括年轻代和年老代。Major GC 发生在老年代的GC，清理老年区，经常会伴随至少一次Minor GC，比Minor GC慢10倍以上。


### [7、为什么使用Executor框架比使用应用创建和管理线程好？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#7为什么使用executor框架比使用应用创建和管理线程好)  


为什么要使用Executor线程池框架

**1、** 每次执行任务创建线程 new Thread()比较消耗性能，创建一个线程是比较耗时、耗资源的。

**2、** 调用 new Thread()创建的线程缺乏管理，被称为野线程，而且可以无限制的创建，线程之间的相互竞争会导致过多占用系统资源而导致系统瘫痪，还有线程之间的频繁交替也会消耗很多系统资源。

**3、** 直接使用new Thread() 启动的线程不利于扩展，比如定时执行、定期执行、定时定期执行、线程中断等都不便实现。

**使用Executor线程池框架的优点 **

**1、** 能复用已存在并空闲的线程从而减少线程对象的创建从而减少了消亡线程的开销。

**2、** 可有效控制最大并发线程数，提高系统资源使用率，同时避免过多资源竞争。

**3、** 框架中已经有定时、定期、单线程、并发数控制等功能。

综上所述使用线程池框架Executor能更好的管理线程、提供系统资源使用率。


### [8、运行时异常与受检异常有何异同？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#8运行时异常与受检异常有何异同)  




异常表示程序运行过程中可能出现的非正常状态，运行时异常表示虚拟机的通常操作中可能遇到的异常，是一种常见运行错误，只要程序设计得没有问题通常就不会发生。受检异常跟程序运行的上下文环境有关，即使程序设计无误，仍然可能因使用的问题而引发。Java编译器要求方法必须声明抛出可能发生的受检异常，但是并不要求必须声明抛出未被捕获的运行时异常。异常和继承一样，是面向对象程序设计中经常被滥用的东西，在_Effective Java_中对异常的使用给出了以下指导原则：

**1、** 不要将异常处理用于正常的控制流（设计良好的API不应该强迫它的调用者为了正常的控制流而使用异常）

**2、** 对可以恢复的情况使用受检异常，对编程错误使用运行时异常

**3、** 避免不必要的使用受检异常（可以通过一些状态检测手段来避免异常的发生）

**4、** 优先使用标准的异常

**5、** 每个方法抛出的异常都要有文档

**6、** 保持异常的原子性

**7、** 不要在catch中忽略掉捕获到的异常


### [9、字节流与字符流的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#9字节流与字符流的区别)  


**1、** 以字节为单位输入输出数据，字节流按照8位传输

**2、** 以字符为单位输入输出数据，字符流按照16位传输


### [10、怎样通过 Java 程序来判断 JVM 是 32 位 还是 64位？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java面试题目大汇总，附参考答案.md#10怎样通过-java-程序来判断-jvm-是-32-位-还是-64位)  


你可以检查某些系统属性如 sun.arch.data.model 或 os.arch 来获取该信息。


### 11、Spring MVC的工作原理是怎样的？
### 12、Java 中的final关键字有哪些用法？
### 13、阐述Spring框架中Bean的生命周期？
### 14、GC 是什么? 为什么要有 GC
### 15、Java中ConcurrentHashMap的并发度是什么？
### 16、38、数据类型之间的转换：
### 17、volatile 类型变量提供什么保证？
### 18、不可变对象对多线程有什么帮助
### 19、分区收集算法
### 20、写一段代码在遍历 ArrayList 时移除一个元素？
### 21、分代收集算法
### 22、CopyOnWriteArrayList 的使用场景?
### 23、ArrayList 和 HashMap 的默认大小是多数？
### 24、如果使用Object作为HashMap的Key，应该怎么办呢？
### 25、同步方法和同步块，哪个是更好的选择?
### 26、线程的 run()和 start()有什么区别？
### 27、实际开发中应用场景哪里用到了模板方法
### 28、为什么要学习工厂设计模式
### 29、描述 Java 中的重载和重写？
### 30、什么是设计模式
### 31、Anonymous Inner Class(匿名内部类)是否可以继承其它类？是否可以实现接口？
### 32、List接口有什么特点？
### 33、线程与进程的区别
### 34、java如何实现多线程之间的通讯和协作？
### 35、ConcurrentHashMap的并发度是什么
### 36、常用的集合类有哪些？
### 37、为什么 Java 中的 String 是不可变的（Immutable）？
### 38、在老年代-标记整理算法
### 39、阐述ArrayList、Vector、LinkedList的存储性能和特性。
### 40、Java中异常分为哪两种？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




