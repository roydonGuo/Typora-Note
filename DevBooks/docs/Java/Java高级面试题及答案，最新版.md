# Java高级面试题及答案，最新版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是接口？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#1什么是接口)  


接口就是某个事物对外提供的一些功能的声明，是一种特殊的java类


### [2、简述正则表达式及其用途。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#2简述正则表达式及其用途。)  




在编写处理字符串的程序时，经常会有查找符合某些复杂规则的字符串的需要。正则表达式就是用于描述这些规则的工具。换句话说，正则表达式就是记录文本规则的代码。

> 说明：计算机诞生初期处理的信息几乎都是数值，但是时过境迁，今天我们使用计算机处理的信息更多的时候不是数值而是字符串，正则表达式就是在进行字符串匹配和处理的时候最为强大的工具，绝大多数语言都提供了对正则表达式的支持。



### [3、生产上如何配置垃圾收集器的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#3生产上如何配置垃圾收集器的)  


首先是内存大小问题，基本上每一个内存区域我都会设置一个上限，来避免溢出问题，比如元空间。通常，堆空间我会设置成操作系统的`2/3`（这是想给其他进程和操作系统预留一些时间），超过8GB的堆优先选用G1。

接下来，我会对JVM进行初步优化。比如根据老年代的对象提升速度，来调整年轻代和老年代之间的比例。

再接下来，就是专项优化，主要判断的依据就是系统容量、访问延迟、吞吐量等。我们的服务是高并发的，所以对STW的时间非常敏感。

我会通过记录详细的GC日志，来找到这个瓶颈点，借用`gceasy`（重点）这样的日志分析工具，很容易定位到问题。之所以选择采用工具，是因为gc日志看起来实在是太麻烦了，gceasy号称是AI学习分析问题，可视化做的较好。


### [4、模式的职责](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#4模式的职责)  


观察者模式主要用于1对N的通知。当一个对象的状态变化时，他需要及时告知一系列对象，令他们做出相应。

**实现有两种方式：**

**1、推：**

每次都会把通知以广播的方式发送给所有观察者，所有的观察者只能被动接收。

**2、拉：**

观察者只要知道有情况即可，至于什么时候获取内容，获取什么内容，都可以自主决定。


### [5、JRE、JDK、JVM 及 JIT 之间有什么不同？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#5jrejdkjvm-及-jit-之间有什么不同)  


JRE 代表 Java 运行时（Java run-time），是运行 Java 引用所必须的。JDK 代表 Java 开发工具（Java development kit），是 Java 程序的开发工具，如 Java编译器，它也包含 JRE。JVM 代表 Java 虚拟机（Java virtual machine），它的责任是运行 Java 应用。JIT 代表即时编译（Just In Time compilation），当代码执行的次数超过一定的阈值时，会将 Java 字节码转换为本地代码，如，主要的热点代码会被准换为本地代码，这样有利大幅度提高 Java 应用的性能。


### [6、Java 面试中其他各式各样的问题](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#6java-面试中其他各式各样的问题)  


这部分包含 Java 中关于 XML 的面试题，正则表达式面试题，Java 错误和异常及序列化面试题


### [7、程序计数器是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#7程序计数器是什么)  


**程序计数器**是一块较小的内存空间，可以看作当前线程所执行字节码的行号指示器。字节码解释器工作时通过改变计数器的值选取下一条执行指令。分支、循环、跳转、线程恢复等功能都需要依赖计数器完成。是唯一在虚拟机规范中没有规定内存溢出情况的区域。

如果线程正在执行 Java 方法，计数器记录正在执行的虚拟机字节码指令地址。如果是本地方法，计数器值为 Undefined。


### [8、Java 内存分配](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#8java-内存分配)  


寄存器：我们无法控制。

静态域：static定义的静态成员。

常量池：编译时被确定并保存在 .class 文件中的（final）常量值和一些文本修饰的符号引用（类和接口的全限定名，字段的名称和描述符，方法和名称和描述符）。

非 RAM 存储：硬盘等永久存储空间。

堆内存：new 创建的对象和数组，由 Java 虚拟机自动垃圾回收器管理,存取速度慢。

栈内存：基本类型的变量和对象的引用变量（堆内存空间的访问地址），速度快，可以共享，但是大小与生存期必须确定，缺乏灵活性。


### [9、新生代与复制算法](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#9新生代与复制算法)  


目前大部分 JVM 的 GC 对于新生代都采取 Copying 算法，因为新生代中每次垃圾回收都要回收大部分对象，即要复制的操作比较少，但通常并不是按照 1：1 来划分新生代。一般将新生代划分为一块较大的 Eden 空间和两个较小的 Survivor 空间(From Space, To Space)，每次使用Eden 空间和其中的一块 Survivor 空间，当进行回收时，将该两块空间中还存活的对象复制到另一块 Survivor 空间中。


### [10、Java 中怎么获取一份线程 dump 文件？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，最新版.md#10java-中怎么获取一份线程-dump-文件)  


在 Linux 下，你可以通过命令 kill -3 PID （Java 进程的进程 ID）来获取 Java 应用的 dump 文件。在 Windows 下，你可以按下 Ctrl + Break 来获取。这样 JVM 就会将线程的 dump 文件打印到标准输出或错误文件中，它可能打印在控制台或者日志文件中，具体位置依赖应用的配置。如果你使用Tomcat。


### 11、那些地方用到了单例模式
### 12、什么是原子类
### 13、永久代
### 14、Semaphore有什么作用
### 15、什么是同步任务？什么是异步任务？
### 16、import java和javax有什么区别
### 17、什么是单例
### 18、什么是线程池？
### 19、程序计数器
### 20、什么是外观模式
### 21、CopyOnWriteArrayList 是什么?
### 22、判断两个对象是否相同，能使用equlas比较吗？
### 23、遇到过元空间溢出吗？
### 24、你能保证 GC 执行吗？
### 25、GC的回收流程是怎样的？
### 26、Collection 和 Collections 有什么区别？
### 27、并发编程有什么缺点
### 28、内存溢出和内存泄漏的区别？
### 29、当父类引用指向子类对象的时候，子类重写了父类方法和属性，那么当访问属性的时候，访问是谁的属性？调用方法时，调用的是谁的方法？
### 30、JRE、JDK、JVM 及 JIT 之间有什么不同？
### 31、解释 Java 堆空间及 GC？
### 32、在Java中CycliBarriar和CountdownLatch有什么区别？
### 33、Java线程池中submit() 和 execute()方法有什么区别？
### 34、什么是内存屏障？
### 35、打印昨天的当前时刻。
### 36、String和StringBuilder、StringBuffer的区别？
### 37、建造者模式的使用场景
### 38、Serial Old 收集器（单线程标记整理算法 ）
### 39、Java Concurrency API中的Lock接口(Lock interface)是什么？对比同步它有什么优势？
### 40、策略模式应用场景





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




