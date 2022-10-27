# Dubbo最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、说说核心的配置有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#1说说核心的配置有哪些)  

| 标签 | 用途 | 解释 |
| --- | --- | --- |
| [dubbo:service/]() | 服务配置 | 用于暴露一个服务，定义服务的元信息，一个服务可以用多个协议暴露，一个服务也可以注册到多个注册中心 |
| [dubbo:reference/]() | 引用配置 | 用于创建一个远程服务代理，一个引用可以指向多个注册中心 |
| [dubbo:protocol/]() | 协议配置 | 用于配置提供服务的协议信息，协议由提供方指定，消费方被动接受 |
| [dubbo:application/]() | 应用配置 | 用于配置当前应用信息，不管该应用是提供者还是消费者 |
| [dubbo:module/]() | 模块配置 | 用于配置当前模块信息，可选 |
| [dubbo:registry/]() | 注册中心配置 | 用于配置连接注册中心相关信息 |
| [dubbo:monitor/]() | 监控中心配置 | 用于配置连接监控中心相关信息，可选 |
| [dubbo:provider/]() | 提供方配置 | 当 ProtocolConfig 和 ServiceConfig 某属性没有配置时，采用此缺省值，可选 |
| [dubbo:consumer/]() | 消费方配置 | 当 ReferenceConfig 某属性没有配置时，采用此缺省值，可选 |
| [dubbo:method/]() | 方法配置 | 用于 ServiceConfig 和 ReferenceConfig 指定方法级的配置信息 |
| [dubbo:argument]() | 参数配置 | 用于指定方法参数配置 |


`如果是SpringBoot项目就只需要注解，或者开Application配置文件！！！`


### [2、Dubbo 支持哪些协议，每种协议的应用场景，优缺点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#2dubbo-支持哪些协议每种协议的应用场景优缺点)  


**1、** dubbo：单一长连接和 NIO 异步通讯，适合大并发小数据量的服务调用，以及消费者远大于提供者。传输协议 TCP，异步， Hessian 序列化；

**2、** rmi：采用 JDK 标准的 rmi 协议实现，传输参数和返回参数对象需要实现Serializable 接口，使用 java 标准序列化机制，使用阻塞式短连接，传输数据包大小混合，消费者和提供者个数差不多，可传文件，传输协议 TCP。多个短连接， TCP 协议传输，同步传输，适用常规的远程服务调用和 rmi 互操作。在依赖低版本的 Common-Collections 包， java 序列化存在安全漏洞；

**3、** http：基于 Http 表单提交的远程调用协议，使用 Spring 的 HttpInvoke 实现。多个短连接，传输协议 HTTP，传入参数大小混合，提供者个数多于消费者，需要给应用程序和浏览器 JS 调用；

**4、** webservice：基于 WebService 的远程调用协议，集成 CXF 实现，提供和原生 WebService 的互操作。多个短连接，基于 HTTP 传输，同步传输，适用系统集成和跨语言调用；

**5、** hessian：集成 Hessian 服务，基于 HTTP 通讯，采用 Servlet 暴露服务，Dubbo 内嵌 Jetty 作为服务器时默认实现，提供与 Hession 服务互操作。多个短连接，同步 HTTP 传输， Hessian 序列化，传入参数较大，提供者大于消费者，提供者压力较大，可传文件；

**6、** Redis：基于 Redis 实现的 RPC 协议


### [3、服务提供者能实现失效踢出是什么原理？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#3服务提供者能实现失效踢出是什么原理)  


服务失效踢出基于zookeeper的临时节点原理。


### [4、PRC架构组件](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#4prc架构组件)  


一个基本的RPC架构里面应该至少包含以下4个组件：

**1、** 客户端（Client）:服务调用方（服务消费者）

**2、** 客户端存根（Client Stub）:存放服务端地址信息，将客户端的请求参数数据信息打包成网络消息，再通过网络传输发送给服务端

**3、** 服务端存根（Server Stub）:接收客户端发送过来的请求消息并进行解包，然后再调用本地服务进行处理4、服务端（Server）:服务的真正提供者

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/026/54/80_4.png#alt=80%5C_4.png)

- 具体调用过程：

**1、** 服务消费者（client客户端）通过调用本地服务的方式调用需要消费的服务；

**2、** 客户端存根（client stub）接收到调用请求后负责将方法、入参等信息序列化（组装）成能够进行网络传输的消息体；

**3、** 客户端存根（client stub）找到远程的服务地址，并且将消息通过网络发送给服务端；

**4、** 服务端存根（server stub）收到消息后进行解码（反序列化操作）；

**5、** 服务端存根（server stub）根据解码结果调用本地的服务进行相关处理；

**6、** 本地服务执行具体业务逻辑并将处理结果返回给服务端存根（server stub）；

**7、** 服务端存根（server stub）将返回结果重新打包成消息（序列化）并通过网络发送至消费方；

**8、** 客户端存根（client stub）接收到消息，并进行解码（反序列化）；

**9、** 服务消费方得到最终结果；

`而RPC框架的实现目标则是将上面的第2-10步完好地封装起来，也就是把调用、编码/解码的过程给封装起来，让用户感觉上像调用本地服务一样的调用远程服务。`


### [5、服务调用是阻塞的吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#5服务调用是阻塞的吗)  


默认是阻塞的，可以异步调用，没有返回值的可以这么做。


### [6、dubbo 服务集群配置（集群容错模式）](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#6dubbo-服务集群配置集群容错模式)  


在集群调用失败时， Dubbo 提供了多种容错方案，缺省为 failover 重试。可以自行扩展集群容错策略

l Failover Cluster(默认)

失败自动切换，当出现失败，重试其它服务器。(缺省)通常用于读操作，

但重试会带来更长延迟。可通过 retries="2"来设置重试次数(不含第一次)。

```
<dubbo:service retries="2" cluster="failover"/>或：<dubbo:reference retries="2" cluster="failover"/>cluster="failover"可以不用写,因为默认就是 failover
```

**Failfast Cluster**

快速失败，只发起一次调用，失败立即报错。通常用于非幂等性的写操作，

比如新增记录。

```
dubbo:service cluster="failfast" />
```

或：

```
<dubbo:reference cluster="failfast" />

cluster="failfast"和 把 cluster="failover"、 retries="0"是一样的效果,retries="0"就是不重
```

Failsafe Cluster失败安全，出现异常时，直接忽略。通常用于写入审计日志等操作。

```
<dubbo:service cluster="failsafe" />
```

或：

```
<dubbo:reference cluster="failsafe" />
```

**Failback Cluster**

失败自动恢复，后台记录失败请求，定时重发。通常用于消息通知操作。

```
<dubbo:service cluster="failback" />
```

或：

```
<dubbo:reference cluster="failback" />
```

Forking Cluster并行调用多个服务器，只要一个成功即返回。通常用于实时性要求较高的读

操作，但需要浪费更多服务资源。可通过 forks="2"来设置最大并行数。

```
<dubbo:service cluster=“forking" forks="2"/>
```

或：

```
<dubbo:reference cluster=“forking" forks="2"/>
```


### [7、Dubbo 核心功能有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#7dubbo-核心功能有哪些)  


**1、** Remoting：网络通信框架，提供对多种NIO框架抽象封装，包括“同步转异步”和“请求-响应”模式的信息交换方式。

**2、** Cluster：服务框架，提供基于接口方法的透明远程过程调用，包括多协议支持，以及软负载均衡，失败容错，地址路由，动态配置等集群支持。

**3、** Registry：服务注册，基于注册中心目录服务，使服务消费方能动态的查找服务提供方，使地址透明，使服务提供方可以平滑增加或减少机器。


### [8、为什么要用Dubbo？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#8为什么要用dubbo)  


随着服务化的进一步发展，服务越来越多，服务之间的调用和依赖关系也越来越复杂，诞生了面向服务的架构体系(SOA)，

也因此衍生出了一系列相应的技术，如对服务提供、服务调用、连接处理、通信协议、序列化方式、服务发现、服务路由、日志输出等行为进行封装的服务框架。

就这样为分布式系统的服务治理框架就出现了，Dubbo也就这样产生了。


### [9、服务调用超时问题怎么解决](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#9服务调用超时问题怎么解决)  


dubbo在调用服务不成功时，默认是会重试两次的。这样在服务端的处理时间超过了设定的超时时间时，就会有重复请求，比如在发邮件时，可能就会发出多份重复邮件，执行注册请求时，就会插入多条重复的注册数据，那么怎么解决超时问题呢？如下

对于核心的服务中心，去除dubbo超时重试机制，并重新评估设置超时时间。 业务处理代码必须放在服务端，客户端只做参数验证和服务调用，不涉及业务流程处理 全局配置实例

<dubbo:provider delay="-1" timeout="6000" retries="0"/>

当然Dubbo的重试机制其实是非常好的QOS保证，它的路由机制，是会帮你把超时的请求路由到其他机器上，而不是本机尝试，所以 dubbo的重试机器也能一定程度的保证服务的质量。但是请一定要综合线上的访问情况，给出综合的评估。


### [10、dubbo 通信协议 dubbo 协议为什么要消费者比提供者个数多？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题大汇总，附答案.md#10dubbo-通信协议-dubbo-协议为什么要消费者比提供者个数多)  


因 dubbo 协议采用单一长连接，假设网络为千兆网卡(1024Mbit=128MByte)，根据测试经验数据每条连接最多只能压满 7MByte(不同的环境可能不一样，供参考)，理论上 1 个服务提供者需要 20个服务消费者才能压满网卡。


### 11、Dubbo服务降级，失败重试怎么做？
### 12、dubbo是什么
### 13、Dubbo 和 Spring Cloud 的区别？
### 14、RPC和SOA、SOAP、REST的区别
### 15、Dubbo 支持分布式事务吗？
### 16、RPC使用了哪些关键技术，序列化
### 17、Dubbo SPI 和 Java SPI 区别？
### 18、为什么要用 Dubbo？
### 19、dubbo 通信协议 dubbo 协议为什么采用异步单一长连接
### 20、Dubbo必须依赖的包有哪些？
### 21、你还了解别的分布式框架吗？
### 22、Dubbo 支持哪些协议，它们的优缺点有哪些？
### 23、Dubbo 使用的是什么通信框架?
### 24、Dubbo 集群的负载均衡有哪些策略?
### 25、Dubbo 推荐什么协议？
### 26、Dubbo 和 Spring Cloud 有什么哪些区别？
### 27、Dubbo telnet 命令能做什么？
### 28、Dubbo集群提供了哪些负载均衡策略？
### 29、dubbo 和 dubbox 之间的区别？
### 30、dubbo 在安全机制方面如何解决的？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




