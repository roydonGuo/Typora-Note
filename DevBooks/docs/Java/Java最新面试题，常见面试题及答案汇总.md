# Java最新面试题，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Java 8 为什么要将永久代(PermGen)替换为元空间(MetaSpace)呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#1java-8-为什么要将永久代permgen替换为元空间metaspace呢)  


整个永久代有一个 JVM 本身设置固定大小上线，无法进行调整，而元空间使用的是直接内存，受本机可用内存的限制，并且永远不会出现java.lang.OutOfMemoryError。你可以使用 -XX：MaxMetaspaceSize 标志设置最大元空间大小，默认值为 unlimited，这意味着它只受系统内存的限制。-XX：MetaspaceSize 调整标志定义元空间的初始大小如果未指定此标志，则 Metaspace 将根据运行时的应用程序需求动态地重新调整大小。


### [2、如何自定义线程线程池?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#2如何自定义线程线程池)  


先看ThreadPoolExecutor（线程池）这个类的构造参数

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/045/42/87_8.png#alt=87%5C_8.png)构造参数参数介绍：

```
corePoolSize 核心线程数量
maximumPoolSize 最大线程数量
keepAliveTime 线程保持时间，N个时间单位
unit 时间单位（比如秒，分）
workQueue 阻塞队列
threadFactory 线程工厂
handler 线程池拒绝策略
```

- 代码示例：

```
package com.lijie;
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;
public class Test001 {
    public static void main(String[] args) {
        //创建线程池
        ThreadPoolExecutor executor = new ThreadPoolExecutor(1, 2, 60L, TimeUnit.SECONDS, new ArrayBlockingQueue < > (3));
        for (int i = 1; i <= 6; i++) {
            TaskThred t1 = new TaskThred("任务" + i);
            //executor.execute(t1);是执行线程方法
            executor.execute(t1);
        }
        //executor.shutdown()不再接受新的任务，并且等待之前提交的任务都执行完再关闭，阻塞队列中的任务不会再执行。
        executor.shutdown();
    }
}
class TaskThred implements Runnable {
    private String taskName;
    public TaskThred(String taskName) {
        this.taskName = taskName;
    }
    public void run() {
        System.out.println(Thread.currentThread().getName() + taskName);
    }
}
```


### [3、类初始化的情况有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#3类初始化的情况有哪些)  


1.
遇到 `new`、`getstatic`、`putstatic` 或 `invokestatic` 字节码指令时，还未初始化。典型场景包括 new 实例化对象、读取或设置静态字段、调用静态方法。

2.
对类反射调用时，还未初始化。

3.
初始化类时，父类还未初始化。

4.
虚拟机启动时，会先初始化包含 main 方法的主类。

5.
使用 JDK7 的动态语言支持时，如果 MethodHandle 实例的解析结果为指定类型的方法句柄且句柄对应的类还未初始化。

6.
口定义了默认方法，如果接口的实现类初始化，接口要在其之前初始化。

7.
其余所有引用类型的方式都不会触发初始化，称为被动引用。被动引用实例：① 子类使用父类的静态字段时，只有父类被初始化。② 通过数组定义使用类。③ 常量在编译期会存入调用类的常量池，不会初始化定义常量的类。

8.
接口和类加载过程的区别：初始化类时如果父类没有初始化需要初始化父类，但接口初始化时不要求父接口初始化，只有在真正使用父接口时（如引用接口中定义的常量）才会初始化。



### [4、Java里有哪些引用类型？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#4java里有哪些引用类型)  


**1、** 强引用 这种引用属于最普通最强硬的一种存在，只有在和 GC Roots 断绝关系时，才会被消灭掉。

**2、** 软引用 软引用用于维护一些可有可无的对象。在内存足够的时候，软引用对象不会被回收，只有在内存不足时，系统则会回收软引用对象，如果回收了软引用对象之后仍然没有足够的内存，才会抛出内存溢出异常。可以看到，这种特性非常适合用在缓存技术上。比如网页缓存、图片缓存等。软引用可以和一个引用队列（ReferenceQueue）联合使用，如果软引用所引用的对象被垃圾回收，Java 虚拟机就会把这个软引用加入到与之关联的引用队列中。

**3、** 弱引用 弱引用对象相比较软引用，要更加无用一些，它拥有更短的生命周期。当JVM进行垃圾回收时，无论内存是否充足，都会回收被弱引用关联的对象。弱引用拥有更短的生命周期，在 Java 中，用 java.lang.ref.WeakReference 类来表示。它的应用场景和软引用类似，可以在一些对内存更加敏感的系统里采用。

**4、** 虚引用 这是一种形同虚设的引用，在现实场景中用的不是很多。虚引用必须和引用队列（ReferenceQueue）联合使用。如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都可能被垃圾回收。实际上，虚引用的 get，总是返回 null。


### [5、JAVA8 与元数据](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#5java8-与元数据)  


在 Java8 中， 永久代已经被移除，被一个称为“元数据区”（元空间）的区域所取代。元空间的本质和永久代类似，元空间与永久代之间最大的区别在于：元空间并不在虚拟机中，而是使用本地内存。因此，默认情况下，元空间的大小仅受本地内存限制。类的元数据放入nativememory, 字符串池和类的静态变量放入 java 堆中， 这样可以加载多少类的元数据就不再由MaxPermSize 控制, 而由系统的实际可用空间来控制。


### [6、引用计数法](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#6引用计数法)  


在 Java 中，引用和对象是有关联的。如果要操作对象则必须用引用进行。因此，很显然一个简单的办法是通过引用计数来判断一个对象是否可以回收。简单说，即一个对象如果没有任何与之关联的引用， 即他们的引用计数都不为 0， 则说明对象不太可能再被用到，那么这个对象就是可回收对象。


### [7、String str=”aaa”,与String str=new String(“aaa”)一样吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#7string-str=aaa,与string-str=new-string“aaa一样吗)  


**1、** 不一样的。因为内存分配的方式不一样。

**2、** 第一种，创建的”aaa”是常量，jvm都将其分配在常量池中。

**3、** 第二种创建的是一个对象，jvm将其值分配在堆内存中。


### [8、Xml的java解析有几种方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#8xml的java解析有几种方式)  


**Java API解析xml主要有两种方式；**

Dom解析：一次性加载整个文档，生成树形结构。在生成的文档对象中，可以对节点进行增删改查的操作。当xml文本当较小的时候，可以使用dom解析。

Sax解析：基于事件的解析方式，解析速度比较快，解析的文档大小理论上是没有限制的。

还有一些开源的技术可以解析xml，dom4j或者jdom。


### [9、为什么 wait(), notify()和 notifyAll()必须在同步方法或者同步块中被调用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#9为什么-wait,-notify和-notifyall必须在同步方法或者同步块中被调用)  


当一个线程需要调用对象的 wait()方法的时候，这个线程必须拥有该对象的锁，接着它就会释放这个对象锁并进入等待状态直到其他线程调用这个对象上的 notify()方法。同样的，当一个线程需要调用对象的 notify()方法时，它会释放这个对象的锁，以便其他在等待的线程就可以得到这个对象锁。由于所有的这些方法都需要线程持有对象的锁，这样就只能通过同步来实现，所以他们只能在同步方法或者同步块中被调用。


### [10、JVM新生代中为什么要分为Eden和Survivor？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题，常见面试题及答案汇总.md#10jvm新生代中为什么要分为eden和survivor)  


如果没有Survivor，Eden区每进行一次Minor GC，存活的对象就会被送到老年代。老年代很快被填满，触发Major GC.老年代的内存空间远大于新生代，进行一次Full GC消耗的时间比Minor GC长得多,所以需要分为Eden和Survivor。Survivor的存在意义，就是减少被送到老年代的对象，进而减少Full GC的发生，Survivor的预筛选保证，只有经历16次Minor GC还能在新生代中存活的对象，才会被送到老年代。设置两个Survivor区最大的好处就是解决了碎片化，刚刚新建的对象在Eden中，经历一次Minor GC，Eden中的存活对象就会被移动到第一块survivor space S0，Eden被清空；等Eden区再满了，就再触发一次Minor GC，Eden和S0中的存活对象又会被复制送入第二块survivor space S1（这个过程非常重要，因为这种复制算法保证了S1中来自S0和Eden两部分的存活对象占用连续的内存空间，避免了碎片化的发生）


### 11、Files的常用方法都有哪些？
### 12、32 位 JVM 和 64 位 JVM 的最大堆内存分别是多数？
### 13、如何开启和查看 GC 日志？
### 14、怎么判断并发队列是阻塞队列还是非阻塞队列
### 15、说说ZGC垃圾收集器的工作原理
### 16、3*0.1 == 0.3 将会返回什么？true 还是 false？
### 17、什么时候会触发FullGC
### 18、[@Before ](/Before ) 和 [@BeforeClass ](/BeforeClass ) 有什么区别？
### 19、什么是线程局部变量？
### 20、Error与Exception区别？
### 21、当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递？
### 22、集合的特点
### 23、React有哪些优化性能是手段?
### 24、虚拟机栈(线程私有)
### 25、为什么要学习设计模式
### 26、构造器注入和 setter 依赖注入，那种方式更好？
### 27、怎样通过 Java 程序来判断 JVM 是 32 位 还是 64 位？
### 28、什么时候使用访问者模式？
### 29、int 和 Integer 哪个会占用更多的内存？
### 30、mixin、hoc、render props、react-hooks的优劣如何？
### 31、如何阻止表单提交
### 32、Java常用包有那些？
### 33、什么是Daemon线程？它有什么意义？
### 34、怎么利用 JUnit 来测试一个方法的异常？
### 35、Js如何跳转到到一个指定页面
### 36、阻塞队列和非阻塞队列区别
### 37、Java 中 interrupted 和 isInterrupted 方法的区别？
### 38、jspservlet中通信作用域有那些？
### 39、重排序遵守的规则
### 40、类、方法、成员变量和局部变量的可用修饰符 -





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




