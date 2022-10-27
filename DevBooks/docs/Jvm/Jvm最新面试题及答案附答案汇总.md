# Jvm最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、如何开启和查看 GC 日志？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#1如何开启和查看-gc-日志)  


**常见的 GC 日志开启参数包括：**

**1、** -Xloggc:filename，指定日志文件路径

**2、** -XX:+PrintGC，打印 GC 基本信息

**3、** -XX:+PrintGCDetails，打印 GC 详细信息

**4、** -XX:+PrintGCTimeStamps，打印 GC 时间戳

**5、** -XX:+PrintGCDateStamps，打印 GC 日期与时间

**6、** -XX:+PrintHeapAtGC，打印 GC 前后的堆、方法区、元空间可用容量变化

**7、** -XX:+PrintTenuringDistribution，打印熬过收集后剩余对象的年龄分布信息，有助于 MaxTenuringThreshold 参数调优设置

**8、** -XX:+PrintAdaptiveSizePolicy，打印收集器自动设置堆空间各分代区域大小、收集目标等自动调节的相关信息

**9、** -XX:+PrintGCApplicationConcurrentTime，打印 GC 过程中用户线程并发时间

**10、** -XX:+PrintGCApplicationStoppedTime，打印 GC 过程中用户线程停顿时间

**11、** -XX:+HeapDumpOnOutOfMemoryError，堆 oom 时自动 dump

**12、** -XX:HeapDumpPath，堆 oom 时 dump 文件路径

Java 9 JVM 日志模块进行了重构，参数格式发生变化，这个需要知道。

GC 日志输出的格式，会随着上面的参数不同而发生变化。关注各个分代的内存使用情况、垃圾回收次数、垃圾回收的原因、垃圾回收占用的时间、吞吐量、用户线程停顿时间。

借助工具可视化工具可以更方便的分析，在线工具 GCeasy；离线版可以使用 GCViewer。

如果现场环境不允许，可以使用 JDK 自带的 jstat 工具监控观察 GC 情况。


### [2、Parallel Scavenge 收集器（多线程复制算法、高效）](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#2parallel-scavenge-收集器多线程复制算法高效)  


Parallel Scavenge 收集器也是一个新生代垃圾收集器，同样使用复制算法，也是一个多线程的垃圾收集器， 它重点关注的是程序达到一个可控制的吞吐量（Thoughput， CPU 用于运行用户代码的时间/CPU 总消耗时间，即吞吐量=运行用户代码时间/(运行用户代码时间+垃圾收集时间)），高吞吐量可以最高效率地利用 CPU 时间，尽快地完成程序的运算任务，主要适用于在后台运算而不需要太多交互的任务。自适应调节策略也是 ParallelScavenge 收集器与 ParNew 收集器的一个重要区别。


### [3、说下有哪些类加载器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#3说下有哪些类加载器)  


Bootstrap ClassLoader（启动类加载器） Extention ClassLoader（扩展类加载器） App ClassLoader（应用类加载器）


### [4、你做过 JVM 调优，说说如何查看 JVM 参数默认值？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#4你做过-jvm-调优说说如何查看-jvm-参数默认值)  


**1、** jps -v 可以查看 jvm 进程显示指定的参数

**2、** 使用 -XX:+PrintFlagsFinal 可以看到 JVM 所有参数的值

**3、** jinfo 可以实时查看和调整虚拟机各项参数


### [5、什么是双亲委派机制？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#5什么是双亲委派机制)  


双亲委派机制的意思是除了顶层的启动类加载器以外，其余的类加载器，在加载之前，都会委派给它的父加载器进行加载。这样一层层向上传递，直到祖先们都无法胜任，它才会真正的加载。


### [6、内存溢出和内存泄漏的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#6内存溢出和内存泄漏的区别)  


内存溢出 OutOfMemory，指程序在申请内存时，没有足够的内存空间供其使用。

内存泄露 Memory Leak，指程序在申请内存后，无法释放已申请的内存空间，内存泄漏最终将导致内存溢出。


### [7、强引用、软引用、弱引用、虚引用是什么，有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#7强引用软引用弱引用虚引用是什么有什么区别)  


**1、** 强引用，就是普通的对象引用关系，如 String s = new String("ConstXiong")

**2、** 软引用，用于维护一些可有可无的对象。只有在内存不足时，系统则会回收软引用对象，如果回收了软引用对象之后仍然没有足够的内存，才会抛出内存溢出异常。SoftReference 实现

**3、** 弱引用，相比软引用来说，要更加无用一些，它拥有更短的生命周期，当 JVM 进行垃圾回收时，无论内存是否充足，都会回收被弱引用关联的对象。WeakReference 实现

**4、** 虚引用是一种形同虚设的引用，在现实场景中用的不是很多，它主要用来跟踪对象被垃圾回收的活动。PhantomReference 实现


### [8、垃圾回收的优点和原理。说说2种回收机制](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#8垃圾回收的优点和原理。说说2种回收机制)  


Java 语言中一个显著的特点就是引入了垃圾回收机制，使 C++ 程序员最头疼的内存管理的问题迎刃而解，它使得 Java 程序员在编写程序的时候不再需要考虑内存管理。由于有个垃圾回收机制，Java 中的对象不再有“作用域”的概念，只有对象的引用才有"作用域"。垃圾回收可以有效的防止内存泄露，有效的使用可以使用的内存。垃圾回收器通常是作为一个单独的低级别的线程运行，不可预知的情况下对内存堆中已经死亡的或者长时间没有使用的对象进行清楚和回收，程序员不能实时的调用垃圾回收器对某个对象或所有对象进行垃圾回收。

**回收机制有分代复制垃圾回收和标记垃圾回收，增量垃圾回收。**


### [9、说一下垃圾分代收集的过程](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#9说一下垃圾分代收集的过程)  


分为新生代和老年代，新生代默认占总空间的 1/3，老年代默认占 2/3。

新生代使用复制算法，有 3 个分区：Eden、To Survivor、From Survivor，它们的默认占比是 8:1:1。

当新生代中的 Eden 区内存不足时，就会触发 Minor GC，过程如下：

**1、** 在 Eden 区执行了第一次 GC 之后，存活的对象会被移动到其中一个 Survivor 分区；

**2、** Eden 区再次 GC，这时会采用复制算法，将 Eden 和 from 区一起清理，存活的对象会被复制到 to 区；

**3、** 移动一次，对象年龄加 1，对象年龄大于一定阀值会直接移动到老年代

**4、** Survivor 区相同年龄所有对象大小的总和 (Survivor 区内存大小 * 这个目标使用率)时，大于或等于该年龄的对象直接进入老年代。其中这个使用率通过 -XX:TargetSurvivorRatio 指定，默认为 50%

**5、** Survivor 区内存不足会发生担保分配

**6、** 超过指定大小的对象可以直接进入老年代

Major GC，指的是老年代的垃圾清理，但并未找到明确说明何时在进行Major GC

FullGC，整个堆的垃圾收集，触发条件：

**1、** 每次晋升到老年代的对象平均大小>老年代剩余空间

**2、** MinorGC后存活的对象超过了老年代剩余空间

**3、** 元空间不足

**4、** System.gc() 可能会引起

**5、** CMS GC异常，promotion failed:MinorGC时，survivor空间放不下，对象只能放入老年代，而老年代也放不下造成；concurrent mode failure:GC时，同时有对象要放入老年代，而老年代空间不足造成

**6、** 堆内存分配很大的对象


### [10、JVM 运行时内存](https://gitee.com/souyunku/DevBooks/blob/master/docs/Jvm/Jvm最新面试题及答案附答案汇总.md#10jvm-运行时内存)  


Java 堆从 GC 的角度还可以细分为: 新生代(Eden 区、 From Survivor 区和 To Survivor 区)和老年代。

**新生代**

是用来存放新生的对象。一般占据堆的 1/3 空间。由于频繁创建对象，所以新生代会频繁触发MinorGC 进行垃圾回收。新生代又分为 Eden区、 ServivorFrom、 ServivorTo 三个区。

**Eden 区**

Java 新对象的出生地（如果新创建的对象占用内存很大，则直接分配到老年代）。当 Eden 区内存不够的时候就会触发 MinorGC，对新生代区进行一次垃圾回收。

**ServivorFrom**

上一次 GC 的幸存者，作为这一次 GC 的被扫描者。

**ServivorTo**

保留了一次 MinorGC 过程中的幸存者。

**MinorGC 的过程（复制->清空->互换）**

MinorGC 采用复制算法。

**eden、 servicorFrom 复制到 ServicorTo，年龄+1**

首先，把 Eden 和 ServivorFrom 区域中存活的对象复制到 ServicorTo 区域（如果有对象的年龄以及达到了老年的标准，则赋值到老年代区），同时把这些对象的年龄+1（如果 ServicorTo 不够位置了就放到老年区）；

**清空 eden、 servicorFrom**

然后，清空 Eden 和 ServicorFrom 中的对象；

**ServicorTo 和 ServicorFrom 互换**

最后， ServicorTo 和 ServicorFrom 互换，原 ServicorTo 成为下一次 GC 时的 ServicorFrom区。


### 11、说说 JVM 如何执行 class 中的字节码。
### 12、运行时栈帧包含哪些结构？
### 13、调优工具
### 14、你了解过哪些垃圾收集器？
### 15、JVM 出现 fullGC 很频繁，怎么去线上排查问题
### 16、你有哪些手段来排查 OOM 的问题？
### 17、32、volatile关键字的原理是什么？干什么用的？
### 18、创建对象的过程是什么？
### 19、怎么打破双亲委派模型？
### 20、JVM 的内存模型以及分区情况和作用
### 21、什么是Java虚拟机？为什么Java被称作是“平台无关的编程语言”？
### 22、什么是happen-before原则？
### 23、什么情况会造成元空间溢出？
### 24、谈谈对 OOM 的认识
### 25、请你谈谈对OOM的认识
### 26、生产上如何配置垃圾收集器的？
### 27、Java 的引用有哪些类型？
### 28、什么情况下会发生栈溢出？
### 29、对象分配规则
### 30、如何判断一个对象是否存活





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




