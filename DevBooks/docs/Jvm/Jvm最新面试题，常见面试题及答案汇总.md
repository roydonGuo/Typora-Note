# Jvm最新面试题，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、类加载有几个过程？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#1类加载有几个过程)  


加载、验证、准备、解析、初始化。


### [2、简述Java的对象结构](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#2简述java的对象结构)  


Java对象由三个部分组成：对象头、实例数据、对齐填充。

对象头由两部分组成，第一部分存储对象自身的运行时数据：哈希码、GC分代年龄、锁标识状态、线程持有的锁、偏向线程ID（一般占32/64 bit）。第二部分是指针类型，指向对象的类元数据类型（即对象代表哪个类）。如果是数组对象，则对象头中还有一部分用来记录数组长度。

实例数据用来存储对象真正的有效信息（包括父类继承下来的和自己定义的）

对齐填充：JVM要求对象起始地址必须是8字节的整数倍（8字节对齐 )


### [3、怎么查看服务器默认的垃圾回收器是哪一个？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#3怎么查看服务器默认的垃圾回收器是哪一个)  


这通常会使用另外一个参数：`-XX:+PrintCommandLineFlags`可以打印所有的参数，包括使用的垃圾回收器。


### [4、JAVA 强引用](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#4java-强引用)  


在 Java 中最常见的就是强引用， 把一个对象赋给一个引用变量，这个引用变量就是一个强引用。当一个对象被强引用变量引用时，它处于可达状态，它是不可能被垃圾回收机制回收的，即使该对象以后永远都不会被用到 JVM 也不会回收。因此强引用是造成 Java 内存泄漏的主要原因之一。


### [5、详细介绍一下JVM内存模型](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#5详细介绍一下jvm内存模型)  


根据 JVM 规范，JVM 内存共分为虚拟机栈、堆、方法区、程序计数器、本地方法栈五个部分。

具体可能会聊聊jdk1.7以前的PermGen（永久代），替换成Metaspace（元空间）

**1、** 原本永久代存储的数据：符号引用(Symbols)转移到了native heap；字面量(interned strings)转移到了java heap；类的静态变量(class statics)转移到了java heap

**2、** Metaspace（元空间）存储的是类的元数据信息（metadata）

**3、** 元空间的本质和永久代类似，都是对JVM规范中方法区的实现。不过元空间与永久代之间最大的区别在于：元空间并不在虚拟机中，而是使用本地内存。

**4、** 替换的好处：一、字符串存在永久代中，容易出现性能问题和内存溢出。二、永久代会为 GC 带来不必要的复杂度，并且回收效率偏低。


### [6、32 位 JVM 和 64 位 JVM 的最大堆内存分别是多数？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#632-位-jvm-和-64-位-jvm-的最大堆内存分别是多数)  


理论上说上 32 位的 JVM 堆内存可以到达 2^32，即 4GB，但实际上会比这个小很多。不同操作系统之间不同，如 Windows 系统大约 1.5GB，Solaris 大约3GB。64 位 JVM 允许指定最大的堆内存，理论上可以达到 2^64，这是一个非常大的数字，实际上你可以指定堆内存大小到 100GB。甚至有的 JVM，如 Azul，堆内存到 1000G 都是可能的。


### [7、HashMap中的key，可以是普通对象么？需要什么注意的地方？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#7hashmap中的key可以是普通对象么需要什么注意的地方)  


Map的key和value都可以是任何类型。但要注意的是，一定要重写它的equals和hashCode方法，否则容易发生内存泄漏。


### [8、你熟悉哪些垃圾收集算法？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#8你熟悉哪些垃圾收集算法)  


标记清除（缺点是碎片化） 复制算法（缺点是浪费空间） 标记整理算法（效率比前两者差） 分代收集算法（老年代一般使用“标记-清除”、“标记-整理”算法，年轻代一般用复制算法）


### [9、GC 垃圾收集器](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#9gc-垃圾收集器)  


Java 堆内存被划分为新生代和年老代两部分，新生代主要使用复制和标记-清除垃圾回收算法；年老代主要使用标记-整理垃圾回收算法，因此 java 虚拟中针对新生代和年老代分别提供了多种不同的垃圾收集器， JDK1.6 中 Sun HotSpot 虚拟机的垃圾收集器


### [10、什么情况发生栈溢出？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题，常见面试题及答案汇总.md#10什么情况发生栈溢出)  


-Xss可以设置线程栈的大小，当线程方法递归调用层次太深或者栈帧中的局部变量过多时，会出现栈溢出错误 java.lang.StackOverflowError


### 11、JAVA软引用
### 12、JVM内存模型
### 13、如何判断对象是否是垃圾？
### 14、程序计数器(线程私有)
### 15、Java 中垃圾收集的方法有哪些
### 16、Java对象创建过程
### 17、简单描述一下（分代）垃圾回收的过程
### 18、被引用的对象就一定能存活吗？
### 19、Serial Old 收集器（单线程标记整理算法 ）
### 20、本地方法栈
### 21、什么是方法内联？
### 22、双亲委派机制可以被违背吗？请举例说明。
### 23、标记整理算法(Mark-Compact)
### 24、哪些是 GC Roots？
### 25、说一下堆内存中对象的分配的基本策略
### 26、JRE、JDK、JVM 及 JIT 之间有什么不同？
### 27、Java 内存分配与回收策率以及 Minor GC 和 Major GC
### 28、如何判断两个类是否相等？
### 29、Java 虚拟机栈的作用？
### 30、能够找到 Reference Chain 的对象，就一定会存活么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




