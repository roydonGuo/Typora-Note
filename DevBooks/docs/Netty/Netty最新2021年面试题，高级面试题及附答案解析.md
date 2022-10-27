# Netty最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Netty 是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#1netty-是什么)  


Netty是 一个异步事件驱动的网络应用程序框架，用于快速开发可维护的高性能协议服务器和客户端。Netty是基于nio的，它封装了jdk的nio，让我们使用起来更加方法灵活。


### [2、NIOEventLoopGroup源码？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#2nioeventloopgroup源码)  


NioEventLoopGroup(其实是MultithreadEventExecutorGroup) 内部维护一个类型为 EventExecutor children [], 默认大小是处理器核数 * 2, 这样就构成了一个线程池，初始化EventExecutor时NioEventLoopGroup重载newChild方法，所以children元素的实际类型为NioEventLoop。

线程启动时调用SingleThreadEventExecutor的构造方法，执行NioEventLoop类的run方法，首先会调用hasTasks()方法判断当前taskQueue是否有元素。如果taskQueue中有元素，执行 selectNow() 方法，最终执行selector.selectNow()，该方法会立即返回。如果taskQueue没有元素，执行 select(oldWakenUp) 方法

select ( oldWakenUp) 方法解决了 Nio 中的 bug，selectCnt 用来记录selector.select方法的执行次数和标识是否执行过selector.selectNow()，若触发了epoll的空轮询bug，则会反复执行selector.select(timeoutMillis)，变量selectCnt 会逐渐变大，当selectCnt 达到阈值（默认512），则执行rebuildSelector方法，进行selector重建，解决cpu占用100%的bug。

rebuildSelector方法先通过openSelector方法创建一个新的selector。然后将old selector的selectionKey执行cancel。最后将old selector的channel重新注册到新的selector中。rebuild后，需要重新执行方法selectNow，检查是否有已ready的selectionKey。

接下来调用processSelectedKeys 方法（处理I/O任务），当selectedKeys != null时，调用processSelectedKeysOptimized方法，迭代 selectedKeys 获取就绪的 IO 事件的selectkey存放在数组selectedKeys中, 然后为每个事件都调用 processSelectedKey 来处理它，processSelectedKey 中分别处理OP_READ；OP_WRITE；OP_CONNECT事件。

最后调用runAllTasks方法（非IO任务），该方法首先会调用fetchFromScheduledTaskQueue方法，把scheduledTaskQueue中已经超过延迟执行时间的任务移到taskQueue中等待被执行，然后依次从taskQueue中取任务执行，每执行64个任务，进行耗时检查，如果已执行时间超过预先设定的执行时间，则停止执行非IO任务，避免非IO任务太多，影响IO任务的执行。

每个NioEventLoop对应一个线程和一个Selector，NioServerSocketChannel会主动注册到某一个NioEventLoop的Selector上，NioEventLoop负责事件轮询。

Outbound 事件都是请求事件, 发起者是 Channel，处理者是 unsafe，通过 Outbound 事件进行通知，传播方向是 tail到head。Inbound 事件发起者是 unsafe，事件的处理者是 Channel, 是通知事件，传播方向是从头到尾。

内存管理机制，首先会预申请一大块内存Arena，Arena由许多Chunk组成，而每个Chunk默认由2048个page组成。Chunk通过AVL树的形式组织Page，每个叶子节点表示一个Page，而中间节点表示内存区域，节点自己记录它在整个Arena中的偏移地址。当区域被分配出去后，中间节点上的标记位会被标记，这样就表示这个中间节点以下的所有节点都已被分配了。大于8k的内存分配在poolChunkList中，而PoolSubpage用于分配小于8k的内存，它会把一个page分割成多段，进行内存分配。

ByteBuf的特点：支持自动扩容（4M），保证put方法不会抛出异常、通过内置的复合缓冲类型，实现零拷贝（zero-copy）；不需要调用flip()来切换读/写模式，读取和写入索引分开；方法链；引用计数基于AtomicIntegerFieldUpdater用于内存回收；PooledByteBuf采用二叉树来实现一个内存池，集中管理内存的分配和释放，不用每次使用都新建一个缓冲区对象。UnpooledHeapByteBuf每次都会新建一个缓冲区对象。


### [3、BIO 是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#3bio-是什么)  


**1、** BIO ，全称 Block-IO ，是一种阻塞 + 同步的通信模式。一种比较传统的通信方式，模式简单，使用方便。但并发处理能力低，通信耗时，依赖网速。

**2、** 原理：服务器通过一个 Acceptor 线程，负责监听客户端请求和为每个客户端创建一个新的线程进行链路处理。典型的一请求一应答模式。若客户端数量增多，频繁地创建和销毁线程会给服务器打开很大的压力。后改良为用线程池的方式代替新增线程，被称为伪异步 IO 。


### [4、Netty 服务端和客户端的启动过程了解么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#4netty-服务端和客户端的启动过程了解么)  


**服务端**

```
        // 1.bossGroup 用于接收连接，workerGroup 用于具体的处理
        EventLoopGroup bossGroup = new NioEventLoopGroup(1);
        EventLoopGroup workerGroup = new NioEventLoopGroup();
        try {
            //2.创建服务端启动引导/辅助类：ServerBootstrap
            ServerBootstrap b = new ServerBootstrap();
            //3.给引导类配置两大线程组,确定了线程模型
            b.group(bossGroup, workerGroup)
                    // (非必备)打印日志
                    .handler(new LoggingHandler(LogLevel.INFO))
                    // 4.指定 IO 模型
                    .channel(NioServerSocketChannel.class)
                    .childHandler(new ChannelInitializer<SocketChannel>() {
                        @Override
                        public void initChannel(SocketChannel ch) {
                            ChannelPipeline p = ch.pipeline();
                            //5.可以自定义客户端消息的业务处理逻辑
                            p.addLast(new HelloServerHandler());
                        }
                    });
            // 6.绑定端口,调用 sync 方法阻塞知道绑定完成
            ChannelFuture f = b.bind(port).sync();
            // 7.阻塞等待直到服务器Channel关闭(closeFuture()方法获取Channel 的CloseFuture对象,然后调用sync()方法)
            f.channel().closeFuture().sync();
        } finally {
            //8.优雅关闭相关线程组资源
            bossGroup.shutdownGracefully();
            workerGroup.shutdownGracefully();
        }
```


### [5、Netty 的高性能表现在哪些方面？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#5netty-的高性能表现在哪些方面)  


**心跳，对服务端：**会定时清除闲置会话 inactive(netty5)，对客户端:用来检测会话是否断开，是否重来，检测网络延迟，其中 idleStateHandler 类 用来检测会话状态

**串行无锁化设计，**即消息的处理尽可能在同一个线程内完成，期间不进行线程切换，这样就避免了多线程竞争和同步锁。表面上看，串行化设计似乎 CPU 利用率不高，并发程度不够。但是，通过调整 NIO 线程池的线程参数，可以同时启动多个串行化的线程并行运行，这种局部无锁化的串行线程设计相比一个队列-多个工作线程模型性能更优。

**可靠性，链路有效性检测：**链路空闲检测机制，读/写空闲超时机制；内存保护机制：通过内存池重用 ByteBuf;ByteBuf 的解码保护；优雅停机：不再接收新消息、退出前的预处理操作、资源的释放操作。

**Netty 安全性：**支持的安全协议：SSL V2 和 V3，TLS，SSL 单向认证、双向认证和第三方 CA证。

**高效并发编程的体现：**volatile 的大量、正确使用；CAS 和原子类的广泛使用；线程安全容器的使用；通过读写锁提升并发性能。IO 通信性能三原则：传输（AIO）、协议（Http）、线程（主从多线程）

**流量整型的作用（变压器）：**防止由于上下游网元性能不均衡导致下游网元被压垮，业务流中断；防止由于通信模块接受消息过快，后端业务线程处理不及时导致撑死问题。

**TCP 参数配置：**SO_RCVBUF 和 SO_SNDBUF：通常建议值为 128K 或者 256K；

SO_TCPNODELAY：NAGLE 算法通过将缓冲区内的小封包自动相连，组成较大的封包，阻止大量小封包的发送阻塞网络，从而提高网络应用效率。但是对于时延敏感的应用场景需要关闭该优化算法；


### [6、Netty 的特点是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#6netty-的特点是什么)  


**1、** 高并发：Netty 是一款基于 NIO（Nonblocking IO，非阻塞IO）开发的网络通信框架，对比于 BIO（Blocking I/O，阻塞IO），他的并发性能得到了很大提高。

**2、** 传输快：Netty 的传输依赖于零拷贝特性，尽量减少不必要的内存拷贝，实现了更高效率的传输。

**3、** 封装好：Netty 封装了 NIO 操作的很多细节，提供了易于使用调用接口。


### [7、NIO 是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#7nio-是什么)  


**1、** NIO ，全称 New IO ，也叫 Non-Block IO ，是一种非阻塞 + 同步的通信模式。Java NIO( New IO 或者 Non Blocking IO ) ，从 Java 1.4 版本开始引入的非阻塞 IO ，用于替换标准( 有些文章也称为传统，或者 Blocking IO 。下文统称为 BIO ) Java IO API 的 IO API 。

**2、** NIO 相对于 BIO 来说一大进步。客户端和服务器之间通过 Channel 通信。NIO 可以在 Channel 进行读写操作。这些 Channel 都会被注册在 Selector 多路复用器上。Selector 通过一个线程不停的轮询这些 Channel 。找出已经准备就绪的 Channel 执行 IO 操作。


### [8、详细看说下 Netty 中的线程模型吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#8详细看说下-netty-中的线程模型吧)  


**单线程模型** ：

一个线程需要执行处理所有的 accept、read、decode、process、encode、send 事件。对于高负载、高并发，并且对性能要求比较高的场景不适用。

对应到 Netty 代码是下面这样的

使用 NioEventLoopGroup 类的无参构造函数设置线程数量的默认值就是 **CPU 核心数 _2_ 。

```
  //1.eventGroup既用于处理客户端连接，又负责具体的处理。
  EventLoopGroup eventGroup = new NioEventLoopGroup(1);
  //2.创建服务端启动引导/辅助类：ServerBootstrap
  ServerBootstrap b = new ServerBootstrap();
            boobtstrap.group(eventGroup, eventGroup)
            //......
```

**多线程模型**

一个 Acceptor 线程只负责监听客户端的连接，一个 NIO 线程池负责具体处理：accept、read、decode、process、encode、send 事件。满足绝大部分应用场景，并发连接量不大的时候没啥问题，但是遇到并发连接大的时候就可能会出现问题，成为性能瓶颈。

对应到 Netty 代码是下面这样的：

```
// 1.bossGroup 用于接收连接，workerGroup 用于具体的处理
EventLoopGroup bossGroup = new NioEventLoopGroup(1);
EventLoopGroup workerGroup = new NioEventLoopGroup();
try {
  //2.创建服务端启动引导/辅助类：ServerBootstrap
  ServerBootstrap b = new ServerBootstrap();
  //3.给引导类配置两大线程组,确定了线程模型
  b.group(bossGroup, workerGroup)
    //......
```

![](https://p6-tt.byteimg.com/large/pgc-image/44965d86138a49f9935046d78d33fd2e#alt=)

**主从多线程模型**

从一个 主线程 NIO 线程池中选择一个线程作为 Acceptor 线程，绑定监听端口，接收客户端连接的连接，其他线程负责后续的接入认证等工作。连接建立完成后，Sub NIO 线程池负责具体处理 I/O 读写。如果多线程模型无法满足你的需求的时候，可以考虑使用主从多线程模型 。

```
// 1.bossGroup 用于接收连接，workerGroup 用于具体的处理
EventLoopGroup bossGroup = new NioEventLoopGroup();
EventLoopGroup workerGroup = new NioEventLoopGroup();
try {
  //2.创建服务端启动引导/辅助类：ServerBootstrap
  ServerBootstrap b = new ServerBootstrap();
  //3.给引导类配置两大线程组,确定了线程模型
  b.group(bossGroup, workerGroup)
    //......
```

![](https://p9-tt.byteimg.com/large/pgc-image/9f9eb75c020a4ea8809fbfebef957145#alt=)


### [9、TCP 粘包 / 拆包的产生原因，应该这么解决](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#9tcp-粘包-/-拆包的产生原因应该这么解决)  


**1、** TCP 是以流的方式来处理数据，所以会导致粘包 / 拆包。

**2、** 拆包：一个完整的包可能会被 TCP 拆分成多个包进行发送。

**3、** 粘包：也可能把小的封装成一个大的数据包发送。

**4、** Netty中提供了多个 Decoder 解析类 用于解决上述问题：

**5、** FixedLengthFrameDecoder 、LengthFieldBasedFrameDecoder ，固定长度是消息头指定消息长度的一种形式，进行粘包拆包处理的。

**6、** LineBasedFrameDecoder 、DelimiterBasedFrameDecoder ，换行是于指定消息边界方式的一种形式，进行消息粘包拆包处理的。


### [10、BIO、NIO 和 AIO 的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Netty/Netty最新2021年面试题，高级面试题及附答案解析.md#10bionio-和-aio-的区别)  


**BIO：**一个连接一个线程，客户端有连接请求时服务器端就需要启动一个线程进行处理。线程开销大。

**伪异步 IO：**将请求连接放入线程池，一对多，但线程还是很宝贵的资源。

**NIO：**一个请求一个线程，但客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有 I/O 请求时才启动一个线程进行处理。

**AIO：**一个有效请求一个线程，客户端的 I/O 请求都是由 OS 先完成了再通知服务器应用去启动线程进行处理。

BIO 是面向流的，NIO 是面向缓冲区的；BIO 的各种流是阻塞的。而 NIO 是非阻塞的；BIO的 Stream 是单向的，而 NIO 的 channel 是双向的。

**NIO 的特点：**事件驱动模型、单线程处理多任务、非阻塞 I/O，I/O 读写不再阻塞，而是返回 0、基于 block 的传输比基于流的传输更高效、更高级的 IO 函数 zero-copy、IO 多路复用大大提高了 Java 网络应用的可伸缩性和实用性。基于 Reactor 线程模型。

在 Reactor 模式中，事件分发器等待某个事件或者可应用或个操作的状态发生，事件分发器就把这个事件传给事先注册的事件处理函数或者回调函数，由后者来做实际的读写操作。如在 Reactor 中实现读：注册读就绪事件和相应的事件处理器、事件分发器等待事件、事件到来，激活分发器，分发器调用事件对应的处理器、事件处理器完成实际的读操作，处理读到的数据，注册新的事件，然后返还控制权。


### 11、了解哪几种序列化协议？
### 12、Netty 中的零拷贝体现在几个方面：
### 13、Netty 支持哪些心跳类型设置？
### 14、了解哪几种序列化协议
### 15、什么是 Reactor 模型
### 16、Netty 的特点？
### 17、Netty 的零拷贝了解么？
### 18、Netty 中有哪种重要组件？
### 19、Netty 的可扩展如何体现
### 20、了解哪几种序列化协议？
### 21、为什么需要心跳机制？Netty 中心跳机制了解么？
### 22、JDK原生NIO程序的问题
### 23、Netty 应用场景了解么？
### 24、如何选择序列化协议？
### 25、Netty为什么要实现内存管理
### 26、原生的NIO存在Epoll Bug有什么BUG、Netty 是怎么解决的
### 27、EventloopGroup 了解么?和 EventLoop 啥关系?
### 28、简单解析一下服务端的创建过程具体是怎样的：
### 29、BIO、NIO 有什么区别？
### 30、Netty 发送消息有几种方式？
### 31、什么是 Netty 的零拷贝？
### 32、客户端代码
### 33、Netty的高可靠体现在哪几方面
### 34、Netty 的应用场景有哪些？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




