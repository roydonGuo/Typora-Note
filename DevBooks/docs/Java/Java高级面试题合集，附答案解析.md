# Java高级面试题合集，附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、说明Tomcat配置了多少个Valve?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#1说明tomcat配置了多少个valve)  


Tomcat配置了四种类型的Valve：

**1、** 访问日志

**2、** 远程地址过滤

**3、** 远程主机过滤器

**4、** 客户请求记录器


### [2、Java中Semaphore是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#2java中semaphore是什么)  


Java中的Semaphore是一种新的同步类，它是一个计数信号。从概念上讲，从概念上讲，信号量维护了一个许可集合。如有必要，在许可可用前会阻塞每一个 acquire()，然后再获取该许可。每个 release()添加一个许可，从而可能释放一个正在阻塞的获取者。但是，不使用实际的许可对象，Semaphore只对可用许可的号码进行计数，并采取相应的行动。信号量常常用于多线程的代码中，比如数据库连接池。


### [3、一个类的构造方法的作用是什么？若一个类没有声明构造方法，改程序能正确执行吗？为什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#3一个类的构造方法的作用是什么若一个类没有声明构造方法改程序能正确执行吗为什么)  


主要作用是完成对类对象的初始化工作。可以执行。因为一个类即使没有声明构造方法也会有默认的不带参数的构造方法。


### [4、请说出与线程同步以及线程调度相关的方法。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#4请说出与线程同步以及线程调度相关的方法。)  




**1、** wait()：使一个线程处于等待（阻塞）状态，并且释放所持有的对象的锁；

**2、** sleep()：使一个正在运行的线程处于睡眠状态，是一个静态方法，调用此方法要处理InterruptedException异常；

**3、** notify()：唤醒一个处于等待状态的线程，当然在调用此方法的时候，并不能确切的唤醒某一个等待状态的线程，而是由JVM确定唤醒哪个线程，而且与优先级无关；

**4、** notityAll()：唤醒所有处于等待状态的线程，该方法并不是将对象的锁给所有线程，而是让它们竞争，只有获得锁的线程才能进入就绪状态；

> 提示：关于Java多线程和并发编程的问题，建议大家看我的另一篇文章[《关于Java并发编程的总结和思考》](http://blog.csdn.net/jackfrued/article/details/44499227)。

> 补充：Java 5通过Lock接口提供了显式的锁机制（explicit lock），增强了灵活性以及对线程的协调。Lock接口中定义了加锁（lock()）和解锁（unlock()）的方法，同时还提供了newCondition()方法来产生用于线程之间通信的Condition对象；此外，Java 5还提供了信号量机制（semaphore），信号量可以用来限制对某个共享资源进行访问的线程的数量。在对资源进行访问之前，线程必须得到信号量的许可（调用Semaphore对象的acquire()方法）；在完成对资源的访问后，线程必须向信号量归还许可（调用Semaphore对象的release()方法）。


下面的例子演示了100个线程同时向一个银行账户中存入1元钱，在没有使用同步机制和使用同步机制情况下的执行情况。

**银行账户类：**

```
/
 * 银行账户
 * @author 骆昊
 *
 */
public class Account {
    private double balance;     // 账户余额

    /
     * 存款
     * @param money 存入金额
     */
    public void deposit(double money) {
        double newBalance = balance + money;
        try {
            Thread.sleep(10);   // 模拟此业务需要一段处理时间
        }
        catch(InterruptedException ex) {
            ex.printStackTrace();
        }
        balance = newBalance;
    }

    /
     * 获得账户余额
     */
    public double getBalance() {
        return balance;
    }
}
```

**存钱线程类：**

```
/
 * 存钱线程
 * @author 骆昊
 *
 */
public class AddMoneyThread implements Runnable {
    private Account account;    // 存入账户
    private double money;       // 存入金额

    public AddMoneyThread(Account account, double money) {
        this.account = account;
        this.money = money;
    }

    @Override
    public void run() {
        account.deposit(money);
    }

}
```

**测试类：**

```
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Test01 {

    public static void main(String[] args) {
        Account account = new Account();
        ExecutorService service = Executors.newFixedThreadPool(100);

        for(int i = 1; i <= 100; i++) {
            service.execute(new AddMoneyThread(account, 1));
        }

        service.shutdown();

        while(!service.isTerminated()) {}

        System.out.println("账户余额: " + account.getBalance());
    }
}
```

在没有同步的情况下，执行结果通常是显示账户余额在10元以下，出现这种状况的原因是，当一个线程A试图存入1元的时候，另外一个线程B也能够进入存款的方法中，线程B读取到的账户余额仍然是线程A存入1元钱之前的账户余额，因此也是在原来的余额0上面做了加1元的操作，同理线程C也会做类似的事情，所以最后100个线程执行结束时，本来期望账户余额为100元，但实际得到的通常在10元以下（很可能是1元哦）。解决这个问题的办法就是同步，当一个线程对银行账户存钱时，需要将此账户锁定，待其操作完成后才允许其他的线程进行操作，代码有如下几种调整方案：

**在银行账户的存款（deposit）方法上同步（synchronized）关键字**

```
/
 * 银行账户
 * @author 骆昊
 *
 */
public class Account {
    private double balance;     // 账户余额

    /
     * 存款
     * @param money 存入金额
     */
    public synchronized void deposit(double money) {
        double newBalance = balance + money;
        try {
            Thread.sleep(10);   // 模拟此业务需要一段处理时间
        }
        catch(InterruptedException ex) {
            ex.printStackTrace();
        }
        balance = newBalance;
    }

    /
     * 获得账户余额
     */
    public double getBalance() {
        return balance;
    }
}
```

**在线程调用存款方法时对银行账户进行同步**

```
/
 * 存钱线程
 * @author 骆昊
 *
 */
public class AddMoneyThread implements Runnable {
    private Account account;    // 存入账户
    private double money;       // 存入金额

    public AddMoneyThread(Account account, double money) {
        this.account = account;
        this.money = money;
    }

    @Override
    public void run() {
        synchronized (account) {
            account.deposit(money); 
        }
    }

}
```

**通过Java 5显示的锁机制，为每个银行账户创建一个锁对象，在存款操作进行加锁和解锁的操作**

```
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/
 * 银行账户
 * 
 * @author 骆昊
 *
 */
public class Account {
    private Lock accountLock = new ReentrantLock();
    private double balance; // 账户余额

    /
     * 存款
     * 
     * @param money
     *            存入金额
     */
    public void deposit(double money) {
        accountLock.lock();
        try {
            double newBalance = balance + money;
            try {
                Thread.sleep(10); // 模拟此业务需要一段处理时间
            }
            catch (InterruptedException ex) {
                ex.printStackTrace();
            }
            balance = newBalance;
        }
        finally {
            accountLock.unlock();
        }
    }

    /
     * 获得账户余额
     */
    public double getBalance() {
        return balance;
    }
}
```

按照上述三种方式对代码进行修改后，重写执行测试代码Test01，将看到最终的账户余额为100元。当然也可以使用Semaphore或CountdownLatch来实现同步。


### [5、正则表达式有那些符号？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#5正则表达式有那些符号)  


**1、** $：匹配字符串结束的位置

**2、** ^：匹配字符串开始的位置

**3、** *：匹配零次或者多次

**4、** +：匹配至少一次

**5、** ?：匹配零次或者一次

**6、** .：匹配除换行符 \n之外的任何单字符

**7、** {n}：n 是一个非负整数，匹配确定的 n 次

**8、** {n,m}：m 和 n 均为非负整数，表示最多和最少匹配次数，其中n <= m

**9、** \w：匹配单个字符(a-z,0-9,_)

**10、** \W：与\w相反

**11、** \d：匹配数字

**12、** \D：与\d相反


### [6、介绍一下 JVM 中垃圾收集器有哪些？ 他们特点分别是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#6介绍一下-jvm-中垃圾收集器有哪些-他们特点分别是什么)  


**新生代垃圾收集器**

**Serial 收集器**

特点： Serial 收集器只能使用一条线程进行垃圾收集工作，并且在进行垃圾收集的时候，所有的工作线程都需要停止工作，等待垃圾收集线程完成以后，其他线程才可以继续工作。

**使用算法：复制算法**

**ParNew 收集器**

特点： ParNew 垃圾收集器是Serial收集器的多线程版本。为了利用 CPU 多核多线程的优势，ParNew 收集器可以运行多个收集线程来进行垃圾收集工作。这样可以提高垃圾收集过程的效率。

**使用算法：复制算法**

**Parallel Scavenge 收集器**

特点： Parallel Scavenge 收集器是一款多线程的垃圾收集器，但是它又和 ParNew 有很大的不同点。

Parallel Scavenge 收集器和其他收集器的关注点不同。其他收集器，比如 ParNew 和 CMS 这些收集器，它们主要关注的是如何缩短垃圾收集的时间。而 Parallel Scavenge 收集器关注的是如何控制系统运行的吞吐量。这里说的吞吐量，指的是 CPU 用于运行应用程序的时间和 CPU 总时间的占比，吞吐量 = 代码运行时间 / （代码运行时间 + 垃圾收集时间）。如果虚拟机运行的总的 CPU 时间是 100 分钟，而用于执行垃圾收集的时间为 1 分钟，那么吞吐量就是 99%。

**使用算法：复制算法**

**老年代垃圾收集器**

**Serial Old 收集器**

特点： Serial Old 收集器是 Serial 收集器的老年代版本。这款收集器主要用于客户端应用程序中作为老年代的垃圾收集器，也可以作为服务端应用程序的垃圾收集器。

**使用算法：标记-整理**

**Parallel Old 收集器**

特点： Parallel Old 收集器是 Parallel Scavenge 收集器的老年代版本这个收集器是在 JDK1.6 版本中出现的，所以在 JDK1.6 之前，新生代的 Parallel Scavenge 只能和 Serial Old 这款单线程的老年代收集器配合使用。Parallel Old 垃圾收集器和 Parallel Scavenge 收集器一样，也是一款关注吞吐量的垃圾收集器，和 Parallel Scavenge 收集器一起配合，可以实现对 Java 堆内存的吞吐量优先的垃圾收集策略。

**使用算法：标记-整理**

**CMS 收集器**

特点： CMS 收集器是目前老年代收集器中比较优秀的垃圾收集器。CMS 是 Concurrent Mark Sweep，从名字可以看出，这是一款使用"标记-清除"算法的并发收集器。

CMS 垃圾收集器是一款以获取最短停顿时间为目标的收集器。如下图所示：

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/05/34/39_3.png#alt=39%5C_3.png)

**从图中可以看出，CMS 收集器的工作过程可以分为 4 个阶段：**

**1、** 初始标记（CMS initial mark）阶段

**2、** 并发标记（CMS concurrent mark）阶段

**3、** 重新标记（CMS remark）阶段

**4、** 并发清除(（CMS concurrent sweep）阶段

使用算法：复制+标记清除

**其他**

**G1 垃圾收集器**

特点： 主要步骤：`初始标记，并发标记，重新标记，复制清除。`

**使用算法：复制 + 标记整理**


### [7、Log4j日志有几个级别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#7log4j日志有几个级别)  


由低到高：debug、info、wran、error


### [8、有哪些类加载器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#8有哪些类加载器)  


自 JDK1.2 起 Java 一直保持三层类加载器：

**启动类加载器**

在 JVM 启动时创建，负责加载最核心的类，例如 Object、System 等。无法被程序直接引用，如果需要把加载委派给启动类加载器，直接使用 null 代替即可，因为启动类加载器通常由操作系统实现，并不存在于 JVM 体系。

**平台类加载器**

从 JDK9 开始从扩展类加载器更换为平台类加载器，负载加载一些扩展的系统类，比如 XML、加密、压缩相关的功能类等。

**应用类加载器**

也称系统类加载器，负责加载用户类路径上的类库，可以直接在代码中使用。如果没有自定义类加载器，一般情况下应用类加载器就是默认的类加载器。自定义类加载器通过继承 ClassLoader 并重写 `findClass` 方法实现。


### [9、描述一下 JVM 加载 class 文件的原理机制](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#9描述一下-jvm-加载-class-文件的原理机制)  


**1、** JVM 中类的装载是由类加载器（ClassLoader）和它的子类来实现的，Java 中各类加载器是一个重要的 Java 运行时系统组件，它负责在运行时查找和装入类文件中的类。

**2、** 由于 Java 的跨平台性，经过编译的 Java 源程序并不是一个可执行程序，而是一个或多个类文件。当 Java 程序需要使用某个类时，JVM 会确保这个类已经被加载、连接（验证、准备和解析）和初始化。类的加载是指把类的.class 文件中的数据读入到内存中，通常是创建一个字节数组读入.class 文件，然后产生与所加载类对应的 Class 对象。

**3、** 加载完成后，Class 对象还不完整，所以此时的类还不可用。当类被加载后就进入连接阶段，这一阶段包括验证、准备（为静态变量分配内存并设置默认的初始值）和解析（将符号引用替换为直接引用）三个步骤。最后 JVM 对类进行初始化，包括：1)如果类存在直接的父类并且这个类还没有被初始化，那么就先初始化父类；2)如果类中存在初始化语句，就依次执行这些初始化语句。

**4、** 类的加载是由类加载器完成的，类加载器包括：根加载器（BootStrap）、扩展加载器（Extension）、系统加载器（System）和用户自定义类加载器（java.lang.ClassLoader 的子类）。

**5、** 从 Java 2（JDK 1.2）开始，类加载过程采取了父亲委托机制（PDM）。PDM 更好的保证了 Java 平台的安全性，在该机制中，JVM 自带的Bootstrap 是根加载器，其他的加载器都有且仅有一个父类加载器。类的加载首先请求父类加载器加载，父类加载器无能为力时才由其子类加载器自行加载。JVM 不会向 Java 程序提供对 Bootstrap 的引用。下面是关于几个类

**加载器的说明：**

**1、** Bootstrap：一般用本地代码实现，负责加载 JVM 基础核心类库（rt.jar）；

**2、** Extension：从 java.ext.dirs 系统属性所指定的目录中加载类库，它的父加载器是 Bootstrap；

**3、** System：又叫应用类加载器，其父类是 Extension。它是应用最广泛的类加载器。它从环境变量 classpath 或者系统属性

java.class.path 所指定的目录中记载类，是用户自定义加载器的默认父加载器。


### [10、Jsp指令有那些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Java/Java高级面试题合集，附答案解析.md#10jsp指令有那些)  


Include

Taglib

Page


### 11、用Java实现阻塞队列
### 12、你对 Time Slice的理解?
### 13、描述一下JVM加载class文件的原理机制？
### 14、Java 中的同步集合与并发集合有什么区别？
### 15、JVM垃圾回收机制，何时触发MinorGC等操作
### 16、对象分配内存的方式有哪些？
### 17、Java中用到的线程调度算法是什么
### 18、什么是FutureTask?使用ExecutorService启动任务。
### 19、对于JDK自带的监控和性能分析工具用过哪些？
### 20、什么是类加载器，类加载器有哪些？
### 21、各种回收算法
### 22、请解释什么是Tomcat Coyote ?
### 23、方法区溢出的原因？
### 24、如何在jsp页面上显示一些特定格式的数字或者日期
### 25、ZGC 了解吗？
### 26、你平时工作中用过的JVM常用基本配置参数有哪些？
### 27、怎么看死锁的线程？
### 28、类的实例化顺序
### 29、比较一下Java和JavaSciprt。
### 30、HashMap中的key，可以是普通对象么？需要什么注意的地方？
### 31、如何判断一个常量是废弃常量 ？
### 32、synchronized关键字的用法？
### 33、面向对象和面向过程的区别
### 34、在使用jdbc的时候，如何防止出现sql注入的问题。
### 35、介绍一下类文件结构吧！
### 36、字符串常量存放在哪个区域？
### 37、什么是多线程环境下的伪共享（false sharing）？
### 38、编写多线程程序有几种实现方式？
### 39、例如： if(a+1.0=4.0)，这样做好吗？
### 40、Get请求与post有什么区别？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




