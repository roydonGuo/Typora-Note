# Java最新面试题及答案整理，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是Web Service（Web服务）](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#1什么是web-serviceweb服务)  


从表面上看，Web Service就是一个应用程序，它向外界暴露出一个能够通过Web进行调用的API。这就是说，你能够用编程的方法透明的调用这个应用程序，不需要了解它的任何细节，跟你使用的编程语言也没有关系。例如可以创建一个提供天气预报的Web Service，那么无论你用哪种编程语言开发的应用都可以通过调用它的API并传入城市信息来获得该城市的天气预报。之所以称之为Web Service，是因为它基于HTTP协议传输数据，这使得运行在不同机器上的不同应用无须借助附加的、专门的第三方软件或硬件，就可相互交换数据或集成。


### [2、内部类与静态内部类的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#2内部类与静态内部类的区别)  


静态内部类相对与外部类是独立存在的，在静态内部类中无法直接访问外部类中变量、方法。如果要访问的话，必须要new一个外部类的对象，使用new出来的对象来访问。但是可以直接访问静态的变量、调用静态的方法；

普通内部类作为外部类一个成员而存在，在普通内部类中可以直接访问外部类属性，调用外部类的方法。

如果外部类要访问内部类的属性或者调用内部类的方法，必须要创建一个内部类的对象，使用该对象访问属性或者调用方法。

如果其他的类要访问普通内部类的属性或者调用普通内部类的方法，必须要在外部类中创建一个普通内部类的对象作为一个属性，外同类可以通过该属性调用普通内部类的方法或者访问普通内部类的属性

如果其他的类要访问静态内部类的属性或者调用静态内部类的方法，直接创建一个静态内部类对象即可。


### [3、什么是代理模式](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#3什么是代理模式)  


通过代理控制对象的访问，可以在这个对象调用方法之前、调用方法之后去处理/添加新的功能。(也就是AO的P微实现)

代理在原有代码乃至原业务流程都不修改的情况下，直接在业务流程中切入新代码，增加新功能，这也和Spring的（面向切面编程）很相似


### [4、32 位 JVM 和 64 位 JVM 的最大堆内存分别是多数？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#432-位-jvm-和-64-位-jvm-的最大堆内存分别是多数)  


理论上说上 32 位的 JVM 堆内存可以到达 2^32，即 4GB，但实际上会比这个小很多。不同操作系统之间不同，如 Windows 系统大约 1.5 GB，Solaris 大约 3GB。64 位 JVM允许指定最大的堆内存，理论上可以达到 2^64，这是一个非常大的数字，实际上你可以指定堆内存大小到 100GB。甚至有的 JVM，如 Azul，堆内存到 1000G 都是可能的。


### [5、重排序实际执行的指令步骤](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#5重排序实际执行的指令步骤)  


![87_5.png][87_5.png]

**1、** 编译器优化的重排序。编译器在不改变单线程程序语义的前提下，可以重新安排语句的执行顺序。

**2、** 指令级并行的重排序。现代处理器采用了指令级并行技术（ILP）来将多条指令重叠执行。如果不存在数据依赖性，处理器可以改变语句对应机器指令的执行顺序。

**3、** 内存系统的重排序。由于处理器使用缓存和读/写缓冲区，这使得加载和存储操作看上去可能是在乱序执行。

这些重排序对于单线程没问题，但是多线程都可能会导致多线程程序出现内存可见性问题。


### [6、invokedynamic指令是干什么的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#6invokedynamic指令是干什么的)  


属于比较高级的题目。没看过虚拟机的一般是不知道的。所以如果你不太熟悉，不要气馁，加油！（小拳拳锤你胸口）。

`invokedynamic`是`Java7`之后新加入的字节码指令，使用它可以实现一些动态类型语言的功能。我们使用的Lambda表达式，在字节码上就是invokedynamic指令实现的。它的功能有点类似反射，但它是使用方法句柄实现的，执行效率更高。


### [7、如何选择单例创建方式](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#7如何选择单例创建方式)  


如果不需要延迟加载单例，可以使用枚举或者饿汉式，相对来说枚举性好于饿汉式。 如果需要延迟加载，可以使用静态内部类或者懒汉式，相对来说静态内部类好于懒韩式。 最好使用饿汉式

- 代码演示

**主要使用懒汉和懒汉式**

**1、** 饿汉式:类初始化时,会立即加载该对象，线程天生安全,调用效率高。

**2、** 懒汉式: 类初始化时,不会初始化该对象,真正需要使用的时候才会创建该对象,具备懒加载功能。

**3、** 静态内部方式:结合了懒汉式和饿汉式各自的优点，真正需要对象的时候才会加载，加载类是线程安全的。

**4、** 枚举单例: 使用枚举实现单例模式 优点:实现简单、调用效率高，枚举本身就是单例，由jvm从根本上提供保障!避免通过反射和反序列化的漏洞， 缺点没有延迟加载。

**5、** 双重检测锁方式 (因为JVM本质重排序的原因，可能会初始化多次，不推荐使用)

- 饿汉式

**饿汉式：**

类初始化时,会立即加载该对象，线程天生安全,调用效率高。

```
package com.lijie;

//饿汉式
public class Demo1 {

    // 类初始化时,会立即加载该对象，线程安全,调用效率高
    private static Demo1 demo1 = new Demo1();

    private Demo1() {
        System.out.println("私有Demo1构造参数初始化");
    }

    public static Demo1 getInstance() {
        return demo1;
    }

    public static void main(String[] args) {
        Demo1 s1 = Demo1.getInstance();
        Demo1 s2 = Demo1.getInstance();
        System.out.println(s1 == s2);
    }
}
```

- 懒汉式

**懒汉式：**

类初始化时,不会初始化该对象,真正需要使用的时候才会创建该对象,具备懒加载功能。

```
package com.lijie;

//懒汉式
public class Demo2 {

    //类初始化时，不会初始化该对象，真正需要使用的时候才会创建该对象。
    private static Demo2 demo2;

    private Demo2() {
        System.out.println("私有Demo2构造参数初始化");
    }

    public synchronized static Demo2 getInstance() {
        if (demo2 == null) {
            demo2 = new Demo2();
        }
        return demo2;
    }

    public static void main(String[] args) {
        Demo2 s1 = Demo2.getInstance();
        Demo2 s2 = Demo2.getInstance();
        System.out.println(s1 == s2);
    }
}
```

- 静态内部类

**静态内部方式：**

结合了懒汉式和饿汉式各自的优点，真正需要对象的时候才会加载，加载类是线程安全的。

```
package com.lijie;

// 静态内部类方式
public class Demo3 {

    private Demo3() {
        System.out.println("私有Demo3构造参数初始化");
    }

    public static class SingletonClassInstance {
        private static final Demo3 DEMO_3 = new Demo3();
    }

    // 方法没有同步
    public static Demo3 getInstance() {
        return SingletonClassInstance.DEMO_3;
    }

    public static void main(String[] args) {
        Demo3 s1 = Demo3.getInstance();
        Demo3 s2 = Demo3.getInstance();
        System.out.println(s1 == s2);
    }
}
```

- 枚举单例式

**枚举单例：**

使用枚举实现单例模式 优点:实现简单、调用效率高，枚举本身就是单例，由jvm从根本上提供保障!避免通过反射和反序列化的漏洞， 缺点没有延迟加载。

```
package com.lijie;

//使用枚举实现单例模式 优点:实现简单、枚举本身就是单例，由jvm从根本上提供保障!避免通过反射和反序列化的漏洞 缺点没有延迟加载
public class Demo4 {

    public static Demo4 getInstance() {
        return Demo.INSTANCE.getInstance();
    }

    public static void main(String[] args) {
        Demo4 s1 = Demo4.getInstance();
        Demo4 s2 = Demo4.getInstance();
        System.out.println(s1 == s2);
    }

    //定义枚举
    private static enum Demo {
        INSTANCE;
        // 枚举元素为单例
        private Demo4 demo4;

        private Demo() {
            System.out.println("枚举Demo私有构造参数");
            demo4 = new Demo4();
        }

        public Demo4 getInstance() {
            return demo4;
        }
    }
}
```

- 双重检测锁方式

**双重检测锁方式**

因为JVM本质重排序的原因，可能会初始化多次，不推荐使用

```
package com.lijie;

//双重检测锁方式
public class Demo5 {

    private static Demo5 demo5;

    private Demo5() {
        System.out.println("私有Demo4构造参数初始化");
    }

    public static Demo5 getInstance() {
        if (demo5 == null) {
            synchronized (Demo5.class) {
                if (demo5 == null) {
                    demo5 = new Demo5();
                }
            }
        }
        return demo5;
    }

    public static void main(String[] args) {
        Demo5 s1 = Demo5.getInstance();
        Demo5 s2 = Demo5.getInstance();
        System.out.println(s1 == s2);
    }
}
```


### [8、Java集合的快速失败机制 “fail-fast”？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#8java集合的快速失败机制-“fail-fast)  


是java集合的一种错误检测机制，当多个线程对集合进行结构上的改变的操作时，有可能会产生 fail-fast 机制。

**例如：**假设存在两个线程（线程**1、** 线程2），线程1通过Iterator在遍历集合A中的元素，在某个时候线程2修改了集合A的结构（是结构上面的修改，而不是简单的修改集合元素的内容），那么这个时候程序就会抛出 ConcurrentModificationException 异常，从而产生fail-fast机制。

**原因：**迭代器在遍历时直接访问集合中的内容，并且在遍历过程中使用一个 modCount 变量。集合在被遍历期间如果内容发生变化，就会改变modCount的值。每当迭代器使用hashNext()/next()遍历下一个元素之前，都会检测modCount变量是否为expectedmodCount值，是的话就返回遍历；否则抛出异常，终止遍历。

**解决办法：**

**1、** 在遍历过程中，所有涉及到改变modCount值得地方全部加上synchronized。

**2、** 使用CopyOnWriteArrayList来替换ArrayList


### [9、如何实现字符串的反转及替换？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#9如何实现字符串的反转及替换)  




方法很多，可以自己写实现也可以使用String或StringBuffer/StringBuilder中的方法。有一道很常见的面试题是用递归实现字符串反转，代码如下所示：

```
    public static String reverse(String originStr) {
        if(originStr == null || originStr.length() <= 1) 
            return originStr;
        return reverse(originStr.substring(1)) + originStr.charAt(0);
    }
```


### [10、Spring开发中的工厂设计模式](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java最新面试题及答案整理，汇总版.md#10spring开发中的工厂设计模式)  


**Spring IOC**

**1、** 看过Spring源码就知道，在Spring IOC容器创建bean的过程是使用了工厂设计模式

**2、** Spring中无论是通过xml配置还是通过配置类还是注解进行创建bean，大部分都是通过简单工厂来进行创建的。

**3、** 当容器拿到了beanName和class类型后，动态的通过反射创建具体的某个对象，最后将创建的对象放到Map中。

**为什么Spring IOC要使用工厂设计模式创建Bean呢**

**1、** 在实际开发中，如果我们A对象调用B，B调用C，C调用D的话我们程序的耦合性就会变高。（耦合大致分为类与类之间的依赖，方法与方法之间的依赖。）

**2、** 在很久以前的三层架构编程时，都是控制层调用业务层，业务层调用数据访问层时，都是是直接new对象，耦合性大大提升，代码重复量很高，对象满天飞

**3、** 为了避免这种情况，Spring使用工厂模式编程，写一个工厂，由工厂创建Bean，以后我们如果要对象就直接管工厂要就可以，剩下的事情不归我们管了。Spring IOC容器的工厂中有个静态的Map集合，是为了让工厂符合单例设计模式，即每个对象只生产一次，生产出对象后就存入到Map集合中，保证了实例不会重复影响程序效率。


### 11、JRE、JDK、JVM 及 JIT 之间有什么不同？
### 12、HTTP的状态码
### 13、线程同步的方法
### 14、类ExampleA继承Exception，类ExampleB继承ExampleA。
### 15、HashMap为什么不直接使用hashCode()处理后的哈希值直接作为table的下标？
### 16、volatile关键字的原理是什么？干什么用的？
### 17、写一个方法，输入一个文件名和一个字符串，统计这个字符串在这个文件中出现的次数。
### 18、线程的状态流转图
### 19、TreeMap 和 TreeSet 在排序时如何比较元素？Collections 工具类中的 sort()方法如何比较元素？
### 20、Java的io流分为哪两种？
### 21、如何解析json对象？
### 22、synchronized 和 ReentrantLock 区别是什么？
### 23、使用Log4j对程序有影响吗？
### 24、在新生代-复制算法
### 25、对象是怎么从年轻代进入老年代的？
### 26、int和Integer有什么区别？
### 27、Java 中的内存映射缓存区是什么？
### 28、你能解释一下里氏替换原则吗?
### 29、类加载的过程是什么？
### 30、说出几点 Java 中使用 Collections 的最佳实践
### 31、程序计数器为什么是私有的?
### 32、为什么需要双亲委派模式？
### 33、HashSet与HashMap的区别
### 34、用 wait-notify 写一段代码来解决生产者-消费者问题？
### 35、谈谈你知道的垃圾收集器
### 36、GC垃圾回收算法与垃圾收集器的关系？
### 37、什么是B/S架构？什么是C/S架构
### 38、什么是事务？事务有那些特点？
### 39、Math.round(11.5) 等于多少？Math.round(-11.5)等于多少？
### 40、什么是happen-before原则？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




