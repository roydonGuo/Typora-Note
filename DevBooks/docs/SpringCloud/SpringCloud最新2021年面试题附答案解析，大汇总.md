# SpringCloud最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是 Hystrix 断路器？我们需要它吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#1什么是-hystrix-断路器我们需要它吗)  


由于某些原因，employee-consumer 公开服务会引发异常。在这种情况下使用 Hystrix 我们定义了一个回退方法。如果在公开服务中发生异常，则回退方法返回一些默认值

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/01/44/45_13.png#alt=45%5C_13.png)

中断，并且员工使用者将一起跳过 firtsPage 方法，并直接调用回退方法。 断路器的目的是给第一页方法或第一页方法可能调用的其他方法留出时间，并导致异常恢复。可能发生的情况是，在负载较小的情况下，导致异常的问题有更好的恢复机会 。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/01/44/45_14.png#alt=45%5C_14.png)


### [2、springcloud如何实现服务的注册?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#2springcloud如何实现服务的注册)  


**1、** 服务发布时，指定对应的服务名,将服务注册到 注册中心(eureka zookeeper)

**2、** 注册中心加@EnableEurekaServer,服务用@EnableDiscoveryClient，然后用ribbon或feign进行服务直接的调用发现。


### [3、微服务架构如何运作？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#3微服务架构如何运作)  


微服务架构具有以下组件：

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_5.png#alt=img%5C_5.png)

图5：微服务 架构 – 微服务面试问题

客户端 – 来自不同设备的不同用户发送请求。

身份提供商 – 验证用户或客户身份并颁发安全令牌。

API网关 – 处理客户端请求。

静态内容 – 容纳系统的所有内容。

管理 – 在节点上平衡服务并识别故障。

服务发现 – 查找微服务之间通信路径的指南。

内容交付网络 – 代理服务器及其数据中心的分布式网络。

远程服务 – 启用驻留在IT设备网络上的远程访问信息。


### [4、Web，RESTful API在微服务中的作用是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#4webrestful-api在微服务中的作用是什么)  


微服务架构基于一个概念，其中所有服务应该能够彼此交互以构建业务功能。因此，要实现这一点，每个微服务必须具有接口。这使得Web API成为微服务的一个非常重要的推动者。RESTful API基于Web的开放网络原则，为构建微服务架构的各个组件之间的接口提供了最合理的模型。


### [5、什么是服务降级](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#5什么是服务降级)  


consumer 端：consumer 如果发现某个provider出现异常情况，⽐如，经常超时(可能是熔断引起的降级)，数据错误，这时，consumer可以采取⼀定的策略，降级provider的逻辑，基本的有直接返回固定的数据。

provider 端：当provider 发现流量激增的时候，为了保护⾃身的稳定性，也可能考虑降级服务。

**1、** 直接给consumer返回固定数据

**2、** 需要实时写⼊数据库的，先缓存到队列⾥，异步写⼊数据库。


### [6、什么是Eureka的自我保护模式，](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#6什么是eureka的自我保护模式)  


默认情况下，如果Eureka Service在一定时间内没有接收到某个微服务的心跳，Eureka Service会进入自我保护模式，在该模式下Eureka Service会保护服务注册表中的信息，不在删除注册表中的数据，当网络故障恢复后，Eureka Servic 节点会自动退出自我保护模式


### [7、什么是不同类型的双因素身份认证？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#7什么是不同类型的双因素身份认证)  


执行双因素身份验证需要三种类型的凭据：

**1、** 一件你知道的事情——比如密码、密码或屏幕锁定模式。

**2、** 您拥有的物理凭证，如OTP、电话或ATM卡，换句话说，您在外部或第三方设备中拥有的任何类型的凭证。

**3、** 您的物理身份–如语音认证或生物特征安全，如指纹或眼睛扫描仪。


### [8、Spring Cloud Sleuth](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#8spring-cloud-sleuth)  


Spring Cloud应用程序的分布式请求链路跟踪，支持使用Zipkin、HTrace和基于日志（例如ELK）的跟踪。


### [9、你所知道微服务的技术栈有哪些？列举一二](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#9你所知道微服务的技术栈有哪些列举一二)  


![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/010/39/49_2.png#alt=49%5C_2.png)


### [10、Spring Cloud Bus](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题附答案解析，大汇总.md#10spring-cloud-bus)  


用于传播集群状态变化的消息总线，使用轻量级消息代理链接分布式系统中的节点，可以用来动态刷新集群中的服务配置。


### 11、如何在SpringBoot应用程序中实现Spring安全性？
### 12、既然Nginx可以实现网关？为什么还需要使用Zuul框架
### 13、Eureka如何 保证AP
### 14、什么是不同类型的微服务测试？
### 15、eureka的缺点：
### 16、Nginx与Ribbon的区别
### 17、多个消费者调⽤同⼀接⼝，eruka默认的分配⽅式是什么？
### 18、什么是 Spring Cloud Bus？
### 19、Eureka怎么实现高可用
### 20、什么是Spring Cloud Zuul（服务网关）
### 21、什么是客户证书？
### 22、Ribbon和Feign的区别？
### 23、微服务测试的主要障碍是什么？
### 24、spring cloud 和dubbo区别?
### 25、21、在Spring MVC应用程序中使用WebMvcTest注释有什么用处？
### 26、我们可以用微服务创建状态机吗？
### 27、微服务之间是如何独⽴通讯的
### 28、如何覆盖SpringBoot项目的默认属性？
### 29、什么是Hystrix?
### 30、服务注册和发现是什么意思？Spring Cloud 如何实现？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




