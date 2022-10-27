# Dubbo最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Dubbo 集群容错有几种方案？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#1dubbo-集群容错有几种方案)  

| 集群容错方案 | 说明 |
| --- | --- |
| Failover Cluster | 失败自动切换，自动重试其它服务器（默认） |
| Failfast Cluster | 快速失败，立即报错，只发起一次调用 |
| Failsafe Cluster | 失败安全，出现异常时，直接忽略 |
| Failback Cluster | 失败自动恢复，记录失败请求，定时重发 |
| Forking Cluster | 并行调用多个服务器，只要一个成功即返回 |
| Broadcast Cluster | 广播逐个调用所有提供者，任意一个报错则报错 |



### [2、Dubbo 的注册中心集群挂掉，发布者和订阅者之间还能通信么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#2dubbo-的注册中心集群挂掉发布者和订阅者之间还能通信么)  


可以通讯。启动 Dubbo 时，消费者会从 Zookeeper 拉取注册的生产者的地址接口等数据，缓存在本地。每次调用时，按照本地存储的地址进行调用。


### [3、Dubbo 能集成 SpringBoot 吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#3dubbo-能集成-springboot-吗)  


可以的


### [4、Dubbo 支持哪些协议，每种协议的应用场景，优缺点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#4dubbo-支持哪些协议每种协议的应用场景优缺点)  


**1、** dubbo：单一长连接和 NIO 异步通讯，适合大并发小数据量的服务调用，以及消费者远大于提供者。传输协议 TCP，异步， Hessian 序列化；

**2、** rmi：采用 JDK 标准的 rmi 协议实现，传输参数和返回参数对象需要实现 Serializable 接口，使用 java 标准序列化机制，使用阻塞式短连接，传输数据包大小混合，消费者和提供者个数差不多，可传文件，传输协议 TCP。多个短连接， TCP 协议传输，同步传输，适用常规的远程服务调用和rmi 互操作。在依赖低版本的 Common-Collections包， java 序列化存在安全漏洞；

**3、** webservice：基于 WebService 的远程调用协议，集成 CXF 实现，提供和原生 WebService 的互操作。多个短连接，基于 HTTP 传输，同步传输，适用系统集成和跨语言调用；

**4、** http：基于 Http 表单提交的远程调用协议，使用 Spring 的HttpInvoke 实现。多个短连接，传输协议 HTTP，传入参数大小混合，提供者个数多于消费者，需要给应用程序和浏览器 JS 调用；

**5、** hessian：集成 Hessian 服务，基于 HTTP 通讯，采用 Servlet 暴露服务， Dubbo 内嵌 Jetty 作为服务器时默认实现，提供与 Hession 服务互操作。多个短连接，同步 HTTP 传输， Hessian 序列化，传入参数较大，提供者大于消费者，提供者压力较大，可传文件；

**6、** memcache：基于 Memcached 实现的 RPC 协议

**7、** Redis：基于 Redis 实现的 RPC 协议


### [5、Dubbo 和 Spring Cloud 的关系？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#5dubbo-和-spring-cloud-的关系)  


Dubbo 是 SOA 时代的产物，它的关注点主要在于服务的调用，流量分发、流量监控和熔断。而 Spring Cloud 诞生于微服务架构时代，考虑的是微服务治理的方方面面，另外由于依托了 Spirng、Spirng Boot 的优势之上，两个框架在开始目标就不一致， Dubbo定位服务治理、 Spirng Cloud 是一个生态。


### [6、dubbo 推荐用什么协议？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#6dubbo-推荐用什么协议)  


默认使用 dubbo 协议。


### [7、Dubbo 核心组件有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#7dubbo-核心组件有哪些)  


![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/026/54/80_1.png#alt=80%5C_1.png)

**1、** Provider：暴露服务的服务提供方

**2、** Consumer：调用远程服务消费方

**3、** Registry：服务注册与发现注册中心

**4、** Monitor：监控中心和访问调用统计

**5、** Container：服务运行容器


### [8、如何解决服务调用链过长的问题？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#8如何解决服务调用链过长的问题)  


Dubbo 可以使用 Pinpoint 和 Apache Skywalking(Incubator) 实现分布式服务追踪，当然还有其他很多方案。


### [9、Dubbo 使用过程中都遇到了些什么问题？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#9dubbo-使用过程中都遇到了些什么问题)  


在注册中心找不到对应的服务,检查service实现类是否添加了@service注解

无法连接到注册中心,检查配置文件中的对应的测试ip是否正确


### [10、同一个服务多个注册的情况下可以直连某一个服务吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题，高级面试题及附答案解析.md#10同一个服务多个注册的情况下可以直连某一个服务吗)  


可以直连，修改配置即可，也可以通过telnet直接某个服务。


### 11、画一画服务注册与发现的流程图？
### 12、Dubbo 有哪些注册中心？
### 13、一般使用什么注册中心？还有别的选择吗？
### 14、Dubbo 的整体架构设计有哪些分层?
### 15、Dubbo 有哪些注册中心？
### 16、服务调用是阻塞的吗？
### 17、Dubbo 和 Dubbox 之间的区别？
### 18、RPC使用了哪些关键技术，序列化和反序列化
### 19、Dubbo 集群的负载均衡有哪些策略
### 20、为什么需要服务治理？
### 21、RPC框架需要解决的问题？
### 22、服务调用是阻塞的吗？
### 23、Dubbo中zookeeper做注册中心，如果注册中心集群都挂掉，者和订阅者之间还能通信么？
### 24、你还了解别的分布式框架吗？
### 25、RPC使用了哪些关键技术，Avro
### 26、一般使用什么注册中心？还有别的选择吗？
### 27、Dubbo Monitor 实现原理？
### 28、同一个服务多个注册的情况下可以直连某一个服务吗？
### 29、Dubbo 服务降级，失败重试怎么做？
### 30、在使用过程中都遇到了些什么问题？
### 31、Dubbo 支持哪些序列化方式？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




