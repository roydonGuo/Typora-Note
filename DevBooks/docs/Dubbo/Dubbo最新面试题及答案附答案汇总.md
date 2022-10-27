# Dubbo最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、你觉得用 Dubbo 好还是 Spring Cloud 好？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#1你觉得用-dubbo-好还是-spring-cloud-好)  


扩展性的问题，没有好坏，只有适合不适合，不过我好像更倾向于使用 Dubbo, Spring Cloud 版本升级太快，组件更新替换太频繁，配置太繁琐，还有很多我觉得是没有 Dubbo 顺手的地方。


### [2、Dubbo Monitor 实现原理？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#2dubbo-monitor-实现原理)  


Consumer端在发起调用之前会先走filter链；provider端在接收到请求时也是先走filter链，然后才进行真正的业务逻辑处理。

默认情况下，在consumer和provider的filter链中都会有Monitorfilter。

**1、** MonitorFilter向DubboMonitor发送数据

**2、** DubboMonitor将数据进行聚合后（默认聚合1min中的统计数据）暂存到ConcurrentMap<Statistics, AtomicReference> statisticsMap，然后使用一个含有3个线程（线程名字：DubboMonitorSendTimer）的线程池每隔1min钟，调用SimpleMonitorService遍历发送statisticsMap中的统计数据，每发送完毕一个，就重置当前的Statistics的AtomicReference

**3、** SimpleMonitorService将这些聚合数据塞入BlockingQueue queue中（队列大写为100000）

**4、** SimpleMonitorService使用一个后台线程（线程名为：DubboMonitorAsyncWriteLogThread）将queue中的数据写入文件（该线程以死循环的形式来写）

**5、** SimpleMonitorService还会使用一个含有1个线程（线程名字：DubboMonitorTimer）的线程池每隔5min钟，将文件中的统计数据画成图表


### [3、RPC使用了哪些关键技术，从调用者的角度看：](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#3rpc使用了哪些关键技术从调用者的角度看：)  


服务的调用者启动的时候根据自己订阅的服务向服务注册中心查找服务提供者的地址等信息；

当服务调用者消费的服务上线或者下线的时候，注册中心会告知该服务的调用者；

服务调用者下线的时候，则取消订阅。


### [4、Dubbo 可以对结果进行缓存吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#4dubbo-可以对结果进行缓存吗)  


为了提高数据访问的速度。Dubbo 提供了声明式缓存，以减少用户加缓存的工作量<dubbo:reference cache=“true” />

其实比普通的配置文件就多了一个标签 cache=“true”


### [5、Dubbo 用到哪些设计模式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#5dubbo-用到哪些设计模式)  


Dubbo框架在初始化和通信过程中使用了多种设计模式，可灵活控制类加载、权限控制等功能。

**工厂模式**

Provider在export服务时，会调用ServiceConfig的export方法。ServiceConfig中有个字段：

```java
private static final Protocol protocol = ExtensionLoader.getExtensionLoader(Protocol.class).getAdaptiveExtension();
```

Dubbo里有很多这种代码。这也是一种工厂模式，只是实现类的获取采用了JDK SPI的机制。这么实现的优点是可扩展性强，想要扩展实现，只需要在classpath下增加个文件就可以了，代码零侵入。另外，像上面的Adaptive实现，可以做到调用时动态决定调用哪个实现，但是由于这种实现采用了动态代理，会造成代码调试比较麻烦，需要分析出实际调用的实现类。

**装饰器模式**

Dubbo在启动和调用阶段都大量使用了装饰器模式。以Provider提供的调用链为例，具体的调用链代码是在ProtocolFilterWrapper的buildInvokerChain完成的，具体是将注解中含有group=provider的Filter实现，按照order排序，最后的调用顺序是：

```java
EchoFilter -> ClassLoaderFilter -> GenericFilter -> ContextFilter -> ExecuteLimitFilter -> TraceFilter -> TimeoutFilter -> MonitorFilter -> ExceptionFilter
```

更确切地说，这里是装饰器和责任链模式的混合使用。例如，EchoFilter的作用是判断是否是回声测试请求，是的话直接返回内容，这是一种责任链的体现。而像ClassLoaderFilter则只是在主功能上添加了功能，更改当前线程的ClassLoader，这是典型的装饰器模式。

**观察者模式**

Dubbo的Provider启动时，需要与注册中心交互，先注册自己的服务，再订阅自己的服务，订阅时，采用了观察者模式，开启一个listener。注册中心会每5秒定时检查是否有服务更新，如果有更新，向该服务的提供者发送一个notify消息，provider接受到notify消息后，即运行NotifyListener的notify方法，执行监听器方法。

**动态代理模式**

Dubbo扩展JDK SPI的类ExtensionLoader的Adaptive实现是典型的动态代理实现。Dubbo需要灵活地控制实现类，即在调用阶段动态地根据参数决定调用哪个实现类，所以采用先生成代理类的方法，能够做到灵活的调用。生成代理类的代码是ExtensionLoader的createAdaptiveExtensionClassCode方法。代理类的主要逻辑是，获取URL参数中指定参数的值作为获取实现类的key。


### [6、Dubbo 如何优雅停机？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#6dubbo-如何优雅停机)  


Dubbo 是通过 JDK 的 ShutdownHook 来完成优雅停机的，所以如果使用kill -9 PID 等强制关闭指令，是不会执行优雅停机的，只有通过 kill PID 时，才会执行。


### [7、RPC使用了哪些关键技术，NIO通信](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#7rpc使用了哪些关键技术nio通信)  


出于并发性能的考虑，传统的阻塞式 IO 显然不太合适，因此我们需要异步的 IO，即 NIO。Java 提供了 NIO 的解决方案，Java 7 也提供了更优秀的 NIO.2 支持。可以选择Netty或者MINA来解决NIO数据传输的问题。


### [8、在使用过程中都遇到了些什么问题？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#8在使用过程中都遇到了些什么问题)  


如序列化问题。


### [9、集群容错怎么做？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#9集群容错怎么做)  


读操作建议使用 Failover 失败自动切换，默认重试两次其他服务器。写操作建议使用 Failfast 快速失败，发一次调用失败就立即报错。


### [10、Dubbo 超时时间怎样设置？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题及答案附答案汇总.md#10dubbo-超时时间怎样设置)  


Dubbo 超时时间设置有两种方式：

服务提供者端设置超时时间，在 Dubbo 的用户文档中，推荐如果能在服务端多配置就尽量多配置，因为服务提供者比消费者更清楚自己提供的服务特性。

服务消费者端设置超时时间，如果在消费者端设置了超时时间，以消费者端为主，即优先级更高。因为服务调用方设置超时时间控制性更灵活。如果消费方超时，服务端线程不会定制，会产生警告。


### 11、说说 Dubbo 服务暴露的过程。
### 12、注册了多个同一样的服务，如果测试指定的某一个服务呢？
### 13、Dubbo 服务降级，失败重试怎么做？
### 14、说说核心的配置有哪些？
### 15、RPC使用了哪些关键技术，Dubbo
### 16、服务上线怎么不影响旧版本？
### 17、dubbo推荐用什么协议？
### 18、Dubbo 支持服务降级吗？
### 19、Dubbo的集群容错方案有哪些？
### 20、dubbo 推荐用什么协议？
### 21、Dubbo 的主要应用场景？
### 22、集群容错怎么做？
### 23、Dubbo 支持哪些协议，每种协议的应用场景，优缺点？
### 24、RPC使用了哪些关键技术，建立通信
### 25、RPC使用了哪些关键技术，动态代理
### 26、服务调用超时会怎么样？
### 27、Dubbo支持服务多协议吗？
### 28、dubbo 服务负载均衡策略？
### 29、dubbo 连接注册中心和直连的区别
### 30、Dubbo 配置文件是如何加载到 Spring 中的？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




