# Java高级面试题及答案，企业真面试题


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、JDK 和 JRE 有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#1jdk-和-jre-有什么区别)  


JDK：Java Development Kit 的简称，java 开发工具包，提供了 java 的开发环境和运行环境。

JRE：Java Runtime Environment 的简称，java 运行环境，为 java 的运行提供了所需环境。 具体来说 JDK 其实包含了 JRE，同时还包含了编译 java 源码的编译器 javac，还包含了很多 java 程序调试和分析的工具。简单来说：如果你需要运行 java 程序，只需安装 JRE 就可以了，如果你需要编写 java 程序，需要安装 JDK。


### [2、能否使用任何类作为 Map 的 key？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#2能否使用任何类作为-map-的-key)  


可以使用任何类作为 Map 的 key，然而在使用之前，需要考虑以下几点：

**1、** 如果类重写了 equals() 方法，也应该重写 hashCode() 方法。

**2、** 类的所有实例需要遵循与 equals() 和 hashCode() 相关的规则。

**3、** 如果一个类没有使用 equals()，不应该在 hashCode() 中使用它。

**4、** 用户自定义 Key 类最佳实践是使之为不可变的，这样 hashCode() 值可以被缓存起来，拥有更好的性能。不可变的类也可以确保 hashCode() 和 equals() 在未来不会改变，这样就会解决与可变相关的问题了。


### [3、简述synchronized 和java.util.concurrent.locks.Lock的异同？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#3简述synchronized-和javautilconcurrentlockslock的异同)  




Lock是Java 5以后引入的新的API，和关键字synchronized相比主要相同点：Lock 能完成synchronized所实现的所有功能；主要不同点：Lock有比synchronized更精确的线程语义和更好的性能，而且不强制性的要求一定要获得锁。synchronized会自动释放锁，而Lock一定要求程序员手工释放，并且最好在finally 块中释放（这是释放外部资源的最好的地方）。


### [4、什么是线程组，为什么在Java中不推荐使用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#4什么是线程组为什么在java中不推荐使用)  


ThreadGroup类，可以把线程归属到某一个线程组中，线程组中可以有线程对象，也可以有线程组，组中还可以有线程，这样的组织结构有点类似于树的形式。

为什么不推荐使用？因为使用有很多的安全隐患吧，没有具体追究，如果需要使用，推荐使用线程池。


### [5、你所知道的web服务器有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#5你所知道的web服务器有哪些)  


**1、** Tomcat

**2、** Jboss

**3、** Weblogic

**4、** Glassfish


### [6、Java中如何实现序列化，有什么意义？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#6java中如何实现序列化有什么意义)  




序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决对象流读写操作时可能引发的问题（如果不进行序列化可能会存在数据乱序的问题）。

要实现序列化，需要让一个类实现Serializable接口，该接口是一个标识性接口，标注该类对象是可被序列化的，然后使用一个输出流来构造一个对象输出流并通过writeObject(Object)方法就可以将实现对象写出（即保存其状态）；如果需要反序列化则可以用一个输入流建立对象输入流，然后通过readObject方法从流中读取对象。序列化除了能够实现对象的持久化之外，还能够用于对象的深度克隆（可以参考第29题）。


### [7、单例模式使用注意事项：](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#7单例模式使用注意事项：)  


**1、** 使用时不能用反射模式创建单例，否则会实例化一个新的对象

**2、** 使用懒单例模式时注意线程安全问题

**3、** 饿单例模式和懒单例模式构造方法都是私有的，因而是不能被继承的，有些单例模式可以被继承（如登记式模式）


### [8、请解释Tomcat的默认端口是什么?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#8请解释tomcat的默认端口是什么)  


Tomcat的默认端口是8080。在本地机器上初始化Tomcat之后，您可以验证Tomcat是否正在运行URL:[http://localhost:8080](http://localhost:8080)


### [9、创建线程的有哪些方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#9创建线程的有哪些方式)  


**1、** 继承Thread类创建线程类

**2、** 通过Runnable接口创建线程类

**3、** 通过Callable和Future创建线程

**4、** 通过线程池创建


### [10、什么是OOP?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题及答案，企业真面试题.md#10什么是oop)  


面向对象编程


### 11、怎么获取 Java 程序使用的内存？堆使用的百分比？
### 12、JVM 选项 -XX:+UseCompressedOops 有什么作用？为什么要使用？
### 13、synchronized和ReentrantLock的区别
### 14、Lock 接口和synchronized 对比同步它有什么优势？
### 15、说说类加载的过程
### 16、接口是什么？为什么要使用接口而不是直接使用具体类？
### 17、什么是并发容器的实现？
### 18、switch 是否能作用在byte 上，是否能作用在long 上，是否能作用在String上？
### 19、Java 中的 TreeMap 是采用什么树实现的？(答案)
### 20、setState到底是异步还是同步?
### 21、阐述final、finally、finalize的区别。
### 22、什么是父类引用指向子类对象？
### 23、ArrayList 和 Vector 的区别是什么？
### 24、线程之间如何通信及线程之间如何同步
### 25、Java中你怎样唤醒一个阻塞的线程？
### 26、你如何确保main()方法所在的线程是Java 程序最后结束的线程？
### 27、java 中的 Math.round(-1.5) 等于多少？
### 28、线程的状态
### 29、FutureTask是什么
### 30、Hashtable 与 HashMap 有什么不同之处？
### 31、Thow与thorws区别
### 32、Java线程具有五中基本状态
### 33、构造方法能不能显式调用？
### 34、哪些是 GC Roots？
### 35、你知道哪些故障处理工具？
### 36、Java 中怎样将 bytes 转换为 long 类型？
### 37、程序计数器有什么作用？
### 38、如果一个类中有抽象方法，那么这个一定是抽象类？
### 39、什么是隐式转换，什么是显式转换
### 40、如何创建守护线程？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




