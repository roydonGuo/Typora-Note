# Java高级面试题，中级面试题，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、线程和进程区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#1线程和进程区别)  


什么是线程和进程?

**进程**

一个在内存中运行的应用程序。 每个正在系统上运行的程序都是一个进程

**线程**

进程中的一个执行任务（控制单元）， 它负责在程序里独立执行。

一个进程至少有一个线程，一个进程可以运行多个线程，多个线程可共享数据

**进程与线程的区别**

**1、** 根本区别：进程是操作系统资源分配的基本单位，而线程是处理器任务调度和执行的基本单位

**2、** 资源开销：每个进程都有独立的代码和数据空间（程序上下文），程序之间的切换会有较大的开销；线程可以看做轻量级的进程，同一类线程共享代码和数据空间，每个线程都有自己独立的运行栈和程序计数器（PC），线程之间切换的开销小。

**3、** 包含关系：如果一个进程内有多个线程，则执行过程不是一条线的，而是多条线（线程）共同完成的；线程是进程的一部分，所以线程也被称为轻权进程或者轻量级进程。

**4、** 内存分配：同一进程的线程共享本进程的地址空间和资源，而进程与进程之间的地址空间和资源是相互独立的

**5、** 影响关系：一个进程崩溃后，在保护模式下不会对其他进程产生影响，但是一个线程崩溃有可能导致整个进程都死掉。所以多进程要比多线程健壮。

**6、** 执行过程：每个独立的进程有程序运行的入口、顺序执行序列和程序出口。但是线程不能独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制，两者均可并发执行


### [2、老年代与标记复制算法](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#2老年代与标记复制算法)  


**而老年代因为每次只回收少量对象，因而采用 Mark-Compact 算法。**

**1、** JAVA 虚拟机提到过的处于方法区的永生代(Permanet Generation)， 它用来存储 class 类，常量，方法描述等。对永生代的回收主要包括废弃常量和无用的类。

**2、** 对象的内存分配主要在新生代的 Eden Space 和 Survivor Space 的 From Space(Survivor 目前存放对象的那一块)，少数情况会直接分配到老生代。

**3、** 当新生代的 Eden Space 和 From Space 空间不足时就会发生一次 GC，进行 GC 后， EdenSpace 和 From Space 区的存活对象会被挪到 To Space，然后将 Eden Space 和 FromSpace 进行清理。

**4、** 如果 To Space 无法足够存储某个对象，则将这个对象存储到老生代。

**5、** 在进行 GC 后，使用的便是 Eden Space 和 To Space 了，如此反复循环。

**6、** 当对象在 Survivor 去躲过一次 GC 后，其年龄就会+1。默认情况下年龄到达 15 的对象会被移到老生代中。


### [3、什么是TreeMap](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#3什么是treemap)  


**1、** TreeMap 是一个**有序的key-value集合**，它是通过红黑树实现的。

**2、** TreeMap基于**红黑树（Red-Black tree）实现**。该映射根据**其键的自然顺序进行排序**，或者根据**创建映射时提供的 Comparator 进行排序**，具体取决于使用的构造方法。

**3、** TreeMap是线程**非同步**的。


### [4、如何停止一个正在运行的线程？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#4如何停止一个正在运行的线程)  


在java中有以下3种方法可以终止正在运行的线程：

**1、** 使用退出标志，使线程正常退出，也就是当run方法完成后线程终止。

**2、** 使用stop方法强行终止，但是不推荐这个方法，因为stop和suspend及resume一样都是过期作废的方法。

**3、** 使用interrupt方法中断线程。


### [5、Java 中，编写多线程程序的时候你会遵循哪些最佳实践？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#5java-中编写多线程程序的时候你会遵循哪些最佳实践)  


这是我在写Java 并发程序的时候遵循的一些最佳实践：

**1、** 给线程命名，这样可以帮助调试。

**2、** 最小化同步的范围，而不是将整个方法同步，只对关键部分做同步。

**3、** 如果可以，更偏向于使用 volatile 而不是 synchronized。

**4、** 使用更高层次的并发工具，而不是使用 wait() 和 notify() 来实现线程间通信，如 BlockingQueue，CountDownLatch 及 Semeaphore。

**5、** 优先使用并发集合，而不是对集合进行同步。并发集合提供更好的可扩展性。


### [6、Java语言采用何种编码方案？有何特点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#6java语言采用何种编码方案有何特点)  


Java语言采用Unicode编码标准，Unicode（标准码），它为每个字符制订了一个唯一的数值，因此在任何的语言，平台，程序都可以放心的使用。


### [7、Java 中你怎样唤醒一个阻塞的线程？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#7java-中你怎样唤醒一个阻塞的线程)  


首先 ，wait()、notify() 方法是针对对象的，调用任意对象的 wait()方法都将导致线程阻塞，阻塞的同时也将释放该对象的锁，相应地，调用任意对象的 notify()方法则将随机解除该对象阻塞的线程，但它需要重新获取该对象的锁，直到获取成功才能往下执行；

其次，wait、notify 方法必须在 synchronized 块或方法中被调用，并且要保证同步块或方法的锁对象与调用 wait、notify 方法的对象是同一个，如此一来在调用 wait 之前当前线程就已经成功获取某对象的锁，执行 wait 阻塞后当前线程就将之前获取的对象锁释放。


### [8、解释内存中的栈(stack)、堆(heap)和方法区(method area)的用法。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#8解释内存中的栈stack堆heap和方法区method-area的用法。)  




通常我们定义一个基本数据类型的变量，一个对象的引用，还有就是函数调用的现场保存都使用JVM中的栈空间；而通过new关键字和构造器创建的对象则放在堆空间，堆是垃圾收集器管理的主要区域，由于现在的垃圾收集器都采用分代收集算法，所以堆空间还可以细分为新生代和老生代，再具体一点可以分为Eden、Survivor（又可分为From Survivor和To Survivor）、Tenured；方法区和堆都是各个线程共享的内存区域，用于存储已经被JVM加载的类信息、常量、静态变量、JIT编译器编译后的代码等数据；程序中的字面量（literal）如直接书写的100、”hello”和常量都是放在常量池中，常量池是方法区的一部分，。栈空间操作起来最快但是栈很小，通常大量的对象都是放在堆空间，栈和堆的大小都可以通过JVM的启动参数来进行调整，栈空间用光了会引发StackOverflowError，而堆和常量池空间不足则会引发OutOfMemoryError。

```
String str = new String("hello");
```

上面的语句中变量str放在栈上，用new创建出来的字符串对象放在堆上，而”hello”这个字面量是放在方法区的。

**补充1：**

较新版本的Java（从Java 6的某个更新开始）中，由于JIT编译器的发展和”逃逸分析”技术的逐渐成熟，栈上分配、标量替换等优化技术使得对象一定分配在堆上这件事情已经变得不那么绝对了。

**补充2：**

运行时常量池相当于Class文件常量池具有动态性，Java语言并不要求常量一定只有编译期间才能产生，运行期间也可以将新的常量放入池中，String类的intern()方法就是这样的。

看看下面代码的执行结果是什么并且比较一下Java 7以前和以后的运行结果是否一致。

```
String s1 = new StringBuilder("go")
    .append("od").toString();
System.out.println(s1.intern() == s1);
String s2 = new StringBuilder("ja")
    .append("va").toString();
System.out.println(s2.intern() == s2);
```


### [9、多线程同步有哪几种方法？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#9多线程同步有哪几种方法)  


Synchronized关键字，Lock锁实现，分布式锁等。


### [10、什么是自旋](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题，中级面试题，大汇总.md#10什么是自旋)  


很多 synchronized 里面的代码只是一些很简单的代码，执行时间非常快，此时等待的线程都加锁可能是一种不太值得的操作，因为线程阻塞涉及到用户态和内核态切换的问题。既然 synchronized 里面的代码执行得非常快，不妨让等待锁的线程不要被阻塞，而是在 synchronized 的边界做忙循环，这就是自旋。如果做了多次循环发现还没有获得锁，再阻塞，这样可能是一种更好的策略。

忙循环：就是程序员用循环让一个线程等待，不像传统方法wait(), sleep() 或 yield() 它们都放弃了CPU控制，而忙循环不会放弃CPU，它就是在运行一个空循环。这么做的目的是为了保留CPU缓存，在多核系统中，一个等待线程醒来的时候可能会在另一个内核运行，这样会重建缓存。为了避免重建缓存和减少等待重建的时间就可以使用它了。


### 11、如何将字符串反转？
### 12、什么是Callable和Future?
### 13、ZGC收集器中的染色指针有什么用？
### 14、TreeMap和TreeSet在排序时如何比较元素？Collections工具类中的sort()方法如何比较元素？
### 15、Java 中，嵌套公共静态类与顶级类有什么不同？
### 16、== 和 equals 的区别是什么？
### 17、你都有哪些手段用来排查内存溢出？
### 18、本地方法栈的作用？
### 19、工厂模式好处
### 20、JVM的引用类型有哪些？
### 21、哪个类包含 clone 方法？是 Cloneable 还是 Object？
### 22、有什么堆外内存的排查思路？
### 23、什么是AQS
### 24、64 位 JVM 中，int 的长度是多数？
### 25、生产环境 CPU 占用过高，你如何解决？
### 26、Java 中，怎么打印出一个字符串的所有排列？
### 27、请解释Tomcat中使用的连接器是什么?
### 28、插入数据时 ArrayList、LinkedList、Vector谁速度较快？
### 29、java中会存在内存泄漏吗，请简单描述。
### 30、什么是方法重载？
### 31、什么是模板方法
### 32、Java中的同步集合与并发集合有什么区别？
### 33、说出 JDK 1.7 中的三个新特性？
### 34、如何使用exception对象？
### 35、Serial 垃圾收集器（单线程、 复制算法）
### 36、为什么wait, notify 和 notifyAll这些方法不在thread类里面？
### 37、as-if-serial规则和happens-before规则的区别
### 38、什么是 CAS
### 39、两个相同的对象会有不同的的 hash code 吗？
### 40、如果对象的引用被置为null，垃圾收集器是否会立即释放对象占用的内存？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




