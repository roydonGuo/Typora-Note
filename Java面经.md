# 基础面试知识

1.Java 的数据类型

答：两种，基础类型和引用类型

引用类型：数组、对象、集合、接口。













# 多线程

MVC：

答：MVC全名是Model View Controller，是模型(model)－视图(view)－控制器(controller)的缩写，一种软件设计典范，用一种业务逻辑、数据、界面显示分离的方法组织代码，将业务逻辑聚集到一个部件里面，在改进和个性化定制界面及用户交互的同时，不需要重新编写业务逻辑。 另：MVC是一种程序开发设计模式,它实现了显示模块与功能模块的分离。提高了程序的可维护性、可移植性、可扩展性与可重用性，降低了程序的开发难度。它主要分模型、视图、控制器三层。 1、模型(model)它是应用程序的主体部分，主要包括业务逻辑模块（web项目中的Action,dao类）和数据模块（pojo类）。模型与数据格式无关，这样一个模型能为多个视图提供数据。由于应用于模型的代码只需写一次就可以被多个视图重用，所以减少了代码的重复性 2、视图(view) 用户与之交互的界面、在web中视图一般由jsp,html组成 3、控制器(controller)接收来自界面的请求 并交给模型进行处理 在这个过程中控制器不做任何处理只是起到了一个连接的作用

***

线程死锁：

答：1.两个或两个以上的线程因为争夺共享资源而造成的相互等待的现象，无外力作用，将无法推进。 当线程进入对象的synchronized代码块时，便占有了资源，直到它退出该代码块或者调用wait方法，才释放资源，在此期间，其他线程将不能进入该代码块。当线程互相持有对方所需要的资源时，会互相等待对方释放资源，如果线程都不主动释放所占有的资源，将产生死锁。 2.从根部解决（从产生死锁的原因入手） 1、互斥使用，即当资源被一个线程使用(占有)时，别的线程不能使用 2、不可抢占，资源请求者不能强制从资源占有者手中夺取资源，资源只能由资源占有者主动释放。 3、请求和保持，即当资源请求者在请求其他的资源的同时保持对原有资源的占有。 4、循环等待，即存在一个等待队列：P1占有P2的资源，P2占有P3的资源，P3占有P1的资源。这样就形成了一个等待环路。

***

如何保证线程安全：

答：多个线程同时操作共享资源时，就会出现线程安全问题。这时就需要我们使用同步方案保证线程安全，常见的保证线程安全的方式有：原子类(底层使用CAS算法实现)、volatile关键字(1.可见性、2.防止指令重排、3.不保证原子性)、Lock类、锁(JUC包下的lock锁)、synchronized关键字等保证线程安全，使用ThreadLocal可以为每一个线程单独保存一份数据，避免了多线程访问共享变量。

保证线程安全的有三种方式：原子类、volatile、锁。
1、原子类：遵循CAS即“比较和替换”规则,比较要更新的值是否等于期望值,如果是则更新,如果不是则失败（单共享变量）
2、volatile关键字：轻量级的synchronized,在多处理器开发中保证了共享变量的“可见性”,从而可以保证单个变量读写时的线程安全（单共享变量）
3、synchronized，java中常用的锁有两种：synchronized+juc包下的lock锁。支持响应中断、支持超时机制、支持以非阻塞的方式获取锁、支持多个条件变量

***

造成线程安全的原因：

答：造成线程安全的原因有三点：` 原子性，可见性，有序性`，那么保证线程安全就从这三个方面考虑。 

原子性：一个或者多个操作在CPU执行的过程中不被中断的特性。线程切换可能造成原子性问题。 

可见性：一个线程对共享变量进行修改，另一个线程能够实时的看见。缓存导致可见性问题。 

有序性：程序执行的顺序按照代码的顺序执行。编译优化可能造成这个问题。 

解决这些问题： Synchronized关键字可以解决原子性、有序性和可见性问题，同时lock和Atomic开头的类也可以解决原子性问题 volatile关键字可以解决可见性问题和有序性问题。通过禁止指令重排来解决有序性问题。 同时解决有序性问题的处理方案两个关键字的处理方式也不相同。

***

现在有T1、T2、T3三个线程，你怎样保证T2在T1执行完后执行，T3在T2执行完后执行？目的是检测你对”join”方法是否熟悉。这个多线程问题比较简单，可以用join方法实现。

答：  thread.Join把指定的线程加入到当前线程，可以将两个交替执行的线程合并为顺序执行的线程。  比如在线程B中调用了线程A的Join()方法，直到线程A执行完毕后，才会继续执行线程B。  想要更深入了解，建议看一下join的源码，也很简单的，使用wait方法实现的。

t.join(); //调用join方法，等待线程t执行完毕 

t.join(1000); //等待 t 线程，等待时间是1000毫秒。

```java
public static void main(String[] args) {
    method01();
    method02();
}
/** * 第一种实现方式，顺序写死在线程代码的内部了，有时候不方便 */
private static void method01() {
    Thread t1 = new Thread(new Runnable() {
        @Override public void run() {
            System.out.println("t1 is finished");
        }
    });
    Thread t2 = new Thread(new Runnable() {
        @Override public void run() {
            try {
                t1.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("t2 is finished");
        }
    });
    Thread t3 = new Thread(new Runnable() {
        @Override public void run() {
            try {
                t2.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("t3 is finished");
        }
    });

    t3.start();
    t2.start();
    t1.start();
}
/** * 第二种实现方式，线程执行顺序可以在方法中调换 */
private static void method02(){
    Runnable runnable = new Runnable() {
        @Override public void run() {
            System.out.println(Thread.currentThread().getName() + "执行完成");
        }
    };
    Thread t1 = new Thread(runnable, "t1");
    Thread t2 = new Thread(runnable, "t2");
    Thread t3 = new Thread(runnable, "t3");
    try {
        t1.start();
        t1.join();
        t2.start();
        t2.join();
        t3.start();
        t3.join();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}
```

***

在java中wait和sleep方法的不同？

答：最大的不同是在等待时wait会释放锁，而sleep一直持有锁。Wait通常被用于线程间交互，sleep通常被用于暂停执行。

***

Java多线程的基础知识： 

– Java的多线程锁是挂在对象上的，并不是在方法上的。即每个对象都有一个锁，当遇到类似synchronized的同步需要时，就会监视(monitor)每个想使用本对象的线程按照一定的规则来访问，规则也就是在同一时间内只能有一个线程能访问此对象。 

– Java中获取锁的单位是线程。当线程A获取了对象B的锁，也就是对象B的持有标记上写的是线程A的唯一标识，在需要同步的情况下的话，只有线程A能访问对象B。 

– Thread常用方法有：start/stop/yield/sleep/interrupt/join等，他们是线程级别的方法，所以并不会太关心锁的具体逻辑。  

– Object的线程有关方法是：wait/wait(事件参数)/notify/notifyAll，他们是对象的方法，所以使用的时候就有点憋屈了，必须当前线程获取了本对象的锁才能使用，否则会报异常。但他们能更细粒度的控制锁，可以释放锁。





