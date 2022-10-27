# Jvm最新面试题及答案整理，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、类加载为什么要使用双亲委派模式，有没有什么场景是打破了这个模式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#1类加载为什么要使用双亲委派模式有没有什么场景是打破了这个模式)  


**双亲委托模型的重要用途是为了解决类载入过程中的安全性问题。**

**1、** 假设有一个开发者自己编写了一个名为`java.lang.Object`的类，想借此欺骗JVM。现在他要使用自定义`ClassLoader`来加载自己编写的`java.lang.Object`类。

**2、** 然而幸运的是，双亲委托模型不会让他成功。因为JVM会优先在`Bootstrap ClassLoader`的路径下找到`java.lang.Object`类，并载入它

Java的类加载是否一定遵循双亲委托模型？

**1、** 在实际开发中，我们可以通过自定义ClassLoader，并重写父类的loadClass方法，来打破这一机制。

**2、** SPI就是打破了双亲委托机制的(SPI：服务提供发现)。


### [2、生产环境 CPU 占用过高，你如何解决？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#2生产环境-cpu-占用过高你如何解决)  


**1、** top + H 指令找出占用 CPU 最高的进程的 pid

**2、** top -H -p

在该进程中找到，哪些线程占用的 CPU 最高的线程，记录下 tid

**3、** jstack -l

threads.txt，导出进程的线程栈信息到文本，导出出现异常的话，加上 -F 参数

**4、** 将 tid 转换为十六进制，在 threads.txt 中搜索，查到对应的线程代码执行栈，在代码中查找占 CPU 比较高的原因。其中 tid 转十六进制，可以借助 Linux 的 printf "%x" tid 指令

我用上述方法查到过，jvm 多条线程疯狂 full gc 导致的CPU 100% 的问题和 JDK1.6 HashMap 并发 put 导致线程 CPU 100% 的问题


### [3、JVM 的内存模型是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#3jvm-的内存模型是什么)  


JVM 试图定义一种统一的内存模型，能将各种底层硬件以及操作系统的内存访问差异进行封装，使 Java 程序在不同硬件以及操作系统上都能达到相同的并发效果。它分为工作内存和主内存，线程无法对主存储器直接进行操作，如果一个线程要和另外一个线程通信，那么只能通过主存进行交换。


### [4、你知道哪些GC类型？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#4你知道哪些gc类型)  


Minor GC：发生在年轻代的 GC。Major GC：发生在老年代的 GC。Full GC：全堆垃圾回收。比如 Metaspace 区引起年轻代和老年代的回收。


### [5、如何判断一个常量是废弃常量 ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#5如何判断一个常量是废弃常量-)  


运行时常量池主要回收的是废弃的常量。假如在常量池中存在字符串 "abc"，如果当前没有任何 String 对象引用该字符串常量的话，就说明常量 "abc" 就是废弃常量，如果这时发生内存回收的话而且有必要的话，"abc" 就会被系统清理出常量池。

### [6、对象的内存布局了解吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#6对象的内存布局了解吗)  


对象在堆内存的存储布局可分为对象头、实例数据和对齐填充。

**对象头**占 12B，包括对象标记和类型指针。对象标记存储对象自身的运行时数据，如哈希码、GC 分代年龄、锁标志、偏向线程 ID 等，这部分占 8B，称为 Mark Word。Mark Word 被设计为动态数据结构，以便在极小的空间存储更多数据，根据对象状态复用存储空间。

类型指针是对象指向它的类型元数据的指针，占 4B。JVM 通过该指针来确定对象是哪个类的实例。

**实例数据**是对象真正存储的有效信息，即本类对象的实例成员变量和所有可见的父类成员变量。存储顺序会受到虚拟机分配策略参数和字段在源码中定义顺序的影响。相同宽度的字段总是被分配到一起存放，在满足该前提条件的情况下父类中定义的变量会出现在子类之前。

**对齐填充**不是必然存在的，仅起占位符作用。虚拟机的自动内存管理系统要求任何对象的大小必须是 8B 的倍数，对象头已被设为 8B 的 1 或 2 倍，如果对象实例数据部分没有对齐，需要对齐填充补全。


### [7、Java对象的布局了解过吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#7java对象的布局了解过吗)  


对象头区域此处存储的信息包括两部分：1、对象自身的运行时数据( MarkWord )，占8字节 存储 hashCode、GC 分代年龄、锁类型标记、偏向锁线程 ID 、 CAS 锁指向线程 LockRecord 的指针等， synconized 锁的机制与这个部分( markwork )密切相关，用 markword 中最低的三位代表锁的状态，其中一位是偏向锁位，另外两位是普通锁位。2、对象类型指针( Class Pointer )，占4字节 对象指向它的类元数据的指针、 JVM 就是通过它来确定是哪个 Class 的实例。

实例数据区域 此处存储的是对象真正有效的信息，比如对象中所有字段的内容

对齐填充区域 JVM 的实现 HostSpot 规定对象的起始地址必须是 8 字节的整数倍，换句话来说，现在 64 位的 OS 往外读取数据的时候一次性读取 64bit 整数倍的数据，也就是 8 个字节，所以 HotSpot 为了高效读取对象，就做了"对齐"，如果一个对象实际占的内存大小不是 8byte 的整数倍时，就"补位"到 8byte 的整数倍。所以对齐填充区域的大小不是固定的。


### [8、谈谈双亲委派模型](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#8谈谈双亲委派模型)  


**1、** Parents Delegation Model，这里的 Parents 翻译成双亲有点不妥，类加载向上传递的过程中只有单亲；parents 更多的是多级向上的意思。

**2、** 除了顶层的启动类加载器，其他的类加载器在加载之前，都会委派给它的父加载器进行加载，一层层向上传递，直到所有父类加载器都无法加载，自己才会加载该类。

**3、** 双亲委派模型，更好地解决了各个类加载器协作时基础类的一致性问题，避免类的重复加载；防止核心API库被随意篡改。

**JDK 9 之前**

**1、** 启动类加载器（Bootstrp ClassLoader），加载 /lib/rt.jar、-Xbootclasspath

**2、** 扩展类加载器（Extension ClassLoader）sun.misc.Launcher$ExtClassLoader，加载 /lib/ext、java.ext.dirs

**3、** 应用程序类加载器（Application ClassLoader，sun.misc.Launcher$AppClassLoader），加载 CLASSPTH、-classpath、-cp、Manifest

**4、** 自定义类加载器

JDK 9 开始 Extension ClassLoader 被 Platform ClassLoader 取代，启动类加载器、平台类加载器、应用程序类加载器全都继承于 jdk.internal.loader.BuiltinClassLoader

类加载代码逻辑

```
protected synchronized Class<?> loadClass(String name, boolean resolve) throws ClassNotFoundException {
  // 首先，检查请求的类是否已经被加载过了
  Class c = findLoadedClass(name);
  if (c == null) {
    try {
      if (parent != null) {
        c = parent.loadClass(name, false);
      } else {
        c = findBootstrapClassOrNull(name);
      }
    } catch (ClassNotFoundException e) {
      // 如果父类加载器抛出ClassNotFoundException
      // 说明父类加载器无法完成加载请求
    }
    if (c == null) {
      // 在父类加载器无法加载时
      // 再调用本身的findClass方法来进行类加载
      c = findClass(name);
    }
  }
  if (resolve) {
    resolveClass(c);
  }
  return c;
}
```


### [9、CMS分为哪几个阶段?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#9cms分为哪几个阶段)  


CMS已经弃用。生活美好，时间有限，不建议再深入研究了。如果碰到问题，直接祭出回收过程即可。

**1、** 初始标记

**2、** 并发标记

**3、** 并发预清理

**4、** 并发可取消的预清理

**5、** 重新标记

**6、** 并发清理

由于《深入理解java虚拟机》一书的流行，面试时省略3、4步一般也是没问题的。


### [10、解释 Java 堆空间及 GC？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案整理，汇总版.md#10解释-java-堆空间及-gc)  


当通过 Java 命令启动 Java 进程的时候，会为它分配内存。内存的一部分用于创建堆空间，当程序中创建对象的时候，就从对空间中分配内存。GC 是 JVM 内部的一个进程，回收无效对象的内存用于将来的分配。


### 11、调优命令有哪些？
### 12、Java 中 WeakReference 与 SoftReference 的区别？
### 13、JRE、JDK、JVM 及 JIT 之间有什么不同？
### 14、CMS都有哪些问题？
### 15、Java 8 为什么要将永久代(PermGen)替换为元空间(MetaSpace)呢？
### 16、64 位 JVM 中，int 的长度是多数？
### 17、介绍一下 JVM 中垃圾收集器有哪些？ 他们特点分别是什么？
### 18、JVM中一次完整的GC流程是怎样的，对象如何晋升到老年代？
### 19、遇到过堆外内存溢出吗？
### 20、对象的访问定位有哪几种方式?
### 21、什么是分布式垃圾回收（DGC）？它是如何工作的？
### 22、遇到过元空间溢出吗？
### 23、说说ZGC垃圾收集器的工作原理
### 24、垃圾回收器的基本原理是什么？垃圾回收器可以马上回收内存吗？有什么办法主动通知虚拟机进行垃圾回收？
### 25、说说类加载的过程
### 26、Serial 垃圾收集器（单线程、 复制算法）
### 27、如何写一段简单的死锁代码？
### 28、如何找到死锁的线程？
### 29、直接内存是什么？
### 30、新生代与复制算法





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




