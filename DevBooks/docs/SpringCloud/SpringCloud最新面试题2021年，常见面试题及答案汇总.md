# SpringCloud最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是Hystrix？它如何实现容错？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#1什么是hystrix它如何实现容错)  


Hystrix是一个延迟和容错库，旨在隔离远程系统，服务和第三方库的访问点，当出现故障是不可避免的故障时，停止级联故障并在复杂的分布式系统中实现弹性。

通常对于使用微服务架构开发的系统，涉及到许多微服务。这些微服务彼此协作。

思考以下微服务

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0814/02/img_2.png#alt=img%5C_2.png)

假设如果上图中的微服务9失败了，那么使用传统方法我们将传播一个异常。但这仍然会导致整个系统崩溃。

随着微服务数量的增加，这个问题变得更加复杂。微服务的数量可以高达1000.这是hystrix出现的地方 我们将使用Hystrix在这种情况下的Fallback方法功能。我们有两个服务employee-consumer使用由employee-consumer公开的服务。

简化图如下所示

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0814/02/img_3.png#alt=img%5C_3.png)

现在假设由于某种原因，employee-producer公开的服务会抛出异常。我们在这种情况下使用Hystrix定义了一个回退方法。这种后备方法应该具有与公开服务相同的返回类型。如果暴露服务中出现异常，则回退方法将返回一些值。


### [2、为什么我们需要微服务容器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#2为什么我们需要微服务容器)  


要管理基于微服务的应用程序，容器是最简单的选择。它帮助用户单独部署和开发。您还可以使用Docker将微服务封装到容器的镜像中。没有任何额外的依赖或工作，微服务可以使用这些元素。


### [3、springcloud和dubbo有哪些区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#3springcloud和dubbo有哪些区别)  


**1、** Dubbo具有调度、发现、监控、治理等功能，⽀持相当丰富的服务治理能⼒。Dubbo架构下，注册中⼼对等集群，并会缓存服务列表已被数据库失效时继续提供发现功能，本身的服务发现结构有很强的可⽤性与健壮性，⾜够⽀持⾼访问量的⽹站。

**2、** 虽然Dubbo ⽀持短连接⼤数据量的服务提供模式，但绝⼤多数情况下都是使⽤⻓连接⼩数据量的模式提供服务使⽤的。所以，对于类似于电商等同步调⽤场景多并且能⽀撑搭建Dubbo 这套⽐较复杂环境的成本的产品⽽⾔，Dubbo 确实是⼀个可以考虑的选择。但如果产品业务中由于后台业务逻辑复杂、时间⻓⽽导致异步逻辑⽐较多的话，可能Dubbo 并不合适。同时，对于⼈⼿不⾜的初创产品⽽⾔，这么重的架构维护起来也不是很⽅便。

**3、** Spring Cloud由众多⼦项⽬组成，如Spring Cloud Config、Spring Cloud Netflix、Spring Cloud Consul 等，提供了搭建分布式系统及微服务常⽤的⼯具，如配置管理、服务发现、断路器、智能路由、微代理、控制总线、⼀次性token、全局锁、选主、分布式会话和集群状态等，满⾜了构建微服务所需的所有解决⽅案。⽐如使⽤Spring Cloud Config 可以实现统⼀配置中⼼，对配置进⾏统⼀管理；使⽤Spring Cloud Netflix 可以实现Netflix 组件的功能 - 服务发现（Eureka）、智能路由（Zuul）、客户端负载均衡（Ribbon）。

**4、** Dubbo 提供了各种 Filter，对于上述中“⽆”的要素，可以通过扩展 Filter 来完善。

**5、** dubbo的开发难度较⼤，原因是dubbo的jar包依赖问题很多⼤型⼯程⽆法解决。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/01/44/45_3.png#alt=45%5C_3.png)


### [4、SpringCloud Config 可以实现实时刷新吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#4springcloud-config-可以实现实时刷新吗)  


springcloud config实时刷新采用SpringCloud Bus消息总线。


### [5、Zookeeper如何 保证CP](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#5zookeeper如何-保证cp)  


当向注册中⼼查询服务列表时，我们可以容忍注册中⼼返回的是⼏分钟以前的注册信息，但不能接受服务直接down掉不可⽤。也就是说，服务注册功能对可⽤性的要求要⾼于⼀致性。但是zk会出现这样⼀种情况，当master节点因为⽹络故障与其他节点失去联系时，剩余节点会重新进⾏leader选举。问题在于，选举leader的时间太⻓，30 ~ 120s, 且选举期间整个zk集群都是不可⽤的，这就导致在选举期间注册服务瘫痪。在云部署的环境下，因⽹络问题使得zk集群失去master节点是较⼤概率会发⽣的事，虽然服务能够最终恢复，但是漫⻓的选举时间导致的注册⻓期不可⽤是不能容忍的。


### [6、微服务之间如何独立通讯的?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#6微服务之间如何独立通讯的)  


同步通信：dobbo通过 RPC 远程过程调用、springcloud通过 REST 接口json调用 等。

异步：消息队列，如：RabbitMq、ActiveM、Kafka 等。


### [7、什么是OAuth？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#7什么是oauth)  


OAuth 代表开放授权协议。这允许通过在HTTP服务上启用客户端应用程序（例如第三方提供商Facebook，GitHub等）来访问资源所有者的资源。因此，您可以在不使用其凭据的情况下与另一个站点共享存储在一个站点上的资源。


### [8、eureka服务注册与发现原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#8eureka服务注册与发现原理)  


**1、** 每30s发送⼼跳检测重新进⾏租约，如果客户端不能多次更新租约，它将在90s内从服务器注册中⼼移除。

**2、** 注册信息和更新会被复制到其他Eureka 节点，来⾃任何区域的客户端可以查找到注册中⼼信息，每30s发⽣⼀次复制来定位他们的服务，并进⾏远程调⽤。

**3、** 客户端还可以缓存⼀些服务实例信息，所以即使Eureka全挂掉，客户端也是可以定位到服务地址的。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/01/44/45_4.png#alt=45%5C_4.png)


### [9、Zuul与Nginx有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#9zuul与nginx有什么区别)  


Zuul是java语言实现的，主要为java服务提供网关服务，尤其在微服务架构中可以更加灵活的对网关进行操作。Nginx是使用C语言实现，性能高于Zuul，但是实现自定义操作需要熟悉lua语言，对程序员要求较高，可以使用Nginx做Zuul集群。


### [10、什么是Spring Cloud？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题2021年，常见面试题及答案汇总.md#10什么是spring-cloud)  


在微服务中，SpringCloud是一个提供与外部系统集成的系统。它是一个敏捷的框架，可以短平快构建应用程序。与有限数量的数据处理相关联，它在微服务体系结构中起着非常重要的作用。 **以下为 Spring Cloud 的核心特性**：

**1、** 版本化/分布式配置。

**2、** 服务注册和发现。

**3、** 服务和服务之间的调用。

**4、** 路由。

**5、** 断路器和负载平衡。

**6、** 分布式消息传递。


### 11、使⽤中碰到的坑
### 12、什么是微服务
### 13、Spring Cloud Netflix(重点，这些组件用的最多)
### 14、什么是耦合和凝聚力？
### 15、Spring Cloud Consul
### 16、什么是Spring Cloud Config?
### 17、负载平衡的意义什么？
### 18、Spring Cloud Config
### 19、SpringCloud 和 Dubbo 有哪些区别?
### 20、架构师在微服务架构中的角色是什么？
### 21、为什么要选择微服务架构？
### 22、熔断的原理，以及如何恢复？
### 23、什么是Semantic监控？
### 24、SpringCloud由什么组成
### 25、SpringCloud的优缺点
### 26、什么是Netflix Feign？它的优点是什么？
### 27、PACT如何运作？
### 28、服务注册和发现是什么意思？Spring Cloud如何实现？
### 29、微服务限流 dubbo限流：dubbo提供了多个和请求相关的filter：ActiveLimitFilter ExecuteLimitFilter TPSLimiterFilter
### 30、Spring Cloud Stream





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




