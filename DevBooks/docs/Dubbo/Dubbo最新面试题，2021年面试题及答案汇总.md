# Dubbo最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Dubbo 集群提供了哪些负载均衡策略？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#1dubbo-集群提供了哪些负载均衡策略)  


**1、** Random LoadBalance: 随机选取提供者策略，有利于动态调整提供者权重。截面碰撞率高，调用次数越多，分布越均匀；

**2、** RoundRobin LoadBalance: 轮循选取提供者策略，平均分布，但是存在请求累积的问题；

**3、** LeastActive LoadBalance: 最少活跃调用策略，解决慢提供者接收更少的请求；

**4、** ConstantHash LoadBalance: 一致性 Hash 策略，使相同参数请求总是发到同一提供者，一台机器宕机，可以基于虚拟节点，分摊至其他提供者，避免引起提供者的剧烈变动；

**5、** 缺省时为 Random 随机调用


### [2、RPC的实现基础？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#2rpc的实现基础)  


**1、** 需要有非常高效的网络通信，比如一般选择Netty作为网络通信框架；

**2、** 需要有比较高效的序列化框架，比如谷歌的Protobuf序列化框架；

**3、** 可靠的寻址方式（主要是提供服务的发现），比如可以使用Zookeeper来注册服务等等；

**4、** 如果是带会话（状态）的RPC调用，还需要有会话和状态保持的功能；


### [3、dubbo 通信协议 dubbo 协议适用范围和适用场景](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#3dubbo-通信协议-dubbo-协议适用范围和适用场景)  


适用范围：传入传出参数数据包较小（建议小于 100K），消费者比提供者个数多，单一消费者无法压满提供者，尽量不要用 dubbo 协议传输大文件或超大字符串。

适用场景：常规远程服务方法调用

dubbo 协议补充：

连接个数：单连接

连接方式：长连接

传输协议：TCP

传输方式：NIO 异步传输

序列化：Hessian 二进制序列化


### [4、Dubbo 是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#4dubbo-是什么)  


Dubbo 是一款高性能、轻量级的开源 RPC 框架，提供服务自动注册、自动发现等高效服务治理方案， 可以和 Spring 框架无缝集成。


### [5、Dubbo 默认采用注册中心？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#5dubbo-默认采用注册中心)  


采用 Zookeeper


### [6、Dubbo SPI 和 Java SPI 区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#6dubbo-spi-和-java-spi-区别)  


**JDK SPI：**

JDK 标准的 SPI 会一次性加载所有的扩展实现，如果有的扩展很耗时，但也没用上，很浪费资源。所以只希望加载某个的实现，就不现实了

**DUBBO SPI：**

**1、** 对 Dubbo 进行扩展，不需要改动 Dubbo 的源码

**2、** 延迟加载，可以一次只加载自己想要加载的扩展实现。

**3、** 增加了对扩展点 IOC 和 AOP 的支持，一个扩展点可以直接 setter 注入其它扩展点。

**4、** Dubbo 的扩展机制能很好的支持第三方 IoC 容器，默认支持 Spring Bean。


### [7、Dubbo 有些哪些注册中心？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#7dubbo-有些哪些注册中心)  


**1、** Multicast 注册中心：Multicast 注册中心不需要任何中心节点，只要广播地址，就能进行服务注册和发现。基于网络中组播传输实现；

**2、** Zookeeper 注册中心：基于分布式协调系统 Zookeeper 实现，采用Zookeeper 的 watch 机制实现数据变更；

**3、** Redis 注册中心：基于 Redis 实现，采用 key/Map 存储，住 key 存储服务名和类型， Map 中 key 存储服务 URL， value 服务过期时间。基于 Redis 的/订阅模式通知数据变更；

**4、** Simple 注册中心


### [8、Dubbo 超时时间怎样设置？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#8dubbo-超时时间怎样设置)  


**Dubbo 超时时间设置有两种方式：**

服务提供者端设置超时时间，在 Dubbo 的用户文档中，推荐如果能在服务端多配置就尽量多配置，因为服务提供者比消费者更清楚自己提供的服务特性。

服务消费者端设置超时时间，如果在消费者端设置了超时时间，以消费者端为主，即优先级更高。因为服务调用方设置超时时间控制性更灵活。如果消费方超时，服务端线程不会定制，会产生警告。


### [9、Dubbo telnet 命令能做什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#9dubbo-telnet-命令能做什么)  


dubbo 服务发布之后，我们可以利用 telnet 命令进行调试、管理。Dubbo2.0.5 以上版本服务提供端口支持 telnet 命令


### [10、Dubbo 和 Spring Cloud 有什么哪些区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题，2021年面试题及答案汇总.md#10dubbo-和-spring-cloud-有什么哪些区别)  


Dubbo 底层是使用 Netty 这样的 NIO 框架，是基于 TCP 协议传输的，配合以 Hession 序列化完成 RPC 通信。

Spring Cloud 是基于 Http 协议 Rest 接口调用远程过程的通信，相对来说 Http 请求会有更大的报文，占的带宽也会更多。但是 REST 相比 RPC 更为灵活，服务提供方和调用方的依赖只依靠一纸契约，不存在代码级别的强依赖，这在强调快速演化的微服务环境下，显得更为合适，至于注重通信速度还是方便灵活性，具体情况具体考虑。


### 11、Dubbo 在安全机制方面是如何解决？
### 12、Dubbo的集群容错方案有哪些？
### 13、服务上线怎么不影响旧版本？
### 14、服务提供者能实现失效踢出是什么原理？
### 15、RPC使用了哪些关键技术，反序列化
### 16、Dubbo 类似的分布式框架还有哪些？
### 17、Dubbo 如何优雅停机？
### 18、Dubbo可以对结果进行缓存吗？
### 19、Dubbo 配置文件是如何加载到Spring中的？
### 20、Dubbo 可以对结果进行缓存吗？
### 21、Dubbo 推荐用什么协议？
### 22、Dubbo 支持分布式事务吗？
### 23、Dubbo 服务注册与发现的流程？
### 24、dubbo 通信协议 dubbo 协议为什么不能传大包；
### 25、默认使用的是什么通信框架，还有别的选择吗?
### 26、Dubbo 与 Spring 的关系？
### 27、如何解决服务调用链过长的问题？
### 28、Dubbo 超时设置有哪些方式？
### 29、Dubbo 的架构设计
### 30、Dubbo 支持哪些序列化方式？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




