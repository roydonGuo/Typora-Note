# SpringCloud最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、设计微服务的最佳实践是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#1设计微服务的最佳实践是什么)  


以下是设计微服务的最佳实践：

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_4.png#alt=img%5C_4.png)

图4：设计微服务的最佳实践 – 微服务访谈问题


### [2、什么是REST / RESTful以及它的用途是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#2什么是rest-/-restful以及它的用途是什么)  


Representational State Transfer（REST）/ RESTful Web服务是一种帮助计算机系统通过Internet进行通信的架构风格。这使得微服务更容易理解和实现。

微服务可以使用或不使用RESTful API实现，但使用RESTful API构建松散耦合的微服务总是更容易。


### [3、什么是feigin？它的优点是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#3什么是feigin它的优点是什么)  


**1、** feign采用的是基于接口的注解

**2、** feign整合了ribbon，具有负载均衡的能力

**3、** 整合了Hystrix，具有熔断的能力

**使用:**

**1、** 添加pom依赖。

**2、** 启动类添加[@EnableFeignClients ](/EnableFeignClients )

**3、** 定义一个接口@FeignClient(name=“xxx”)指定调用哪个服务


### [4、负载平衡的意义什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#4负载平衡的意义什么)  


在计算中，负载平衡可以改善跨计算机，计算机集群，网络链接，中央处理单元或磁盘驱动器等多种计算资源的工作负载分布。负载平衡旨在优化资源使用，最大化吞吐量，最小化响应时间并避免任何单一资源的过载。使用多个组件进行负载平衡而不是单个组件可能会通过冗余来提高可靠性和可用性。负载平衡通常涉及专用软件或硬件，例如多层交换机或域名系统服务器进程。


### [5、服务网关的作用](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#5服务网关的作用)  


**1、** 简化客户端调用复杂度，统一处理外部请求。

**2、** 数据裁剪以及聚合，根据不同的接口需求，对数据加工后对外。

**3、** 多渠道支持，针对不同的客户端提供不同的网关支持。

**4、** 遗留系统的微服务化改造，可以作为新老系统的中转组件。

**5、** 统一处理调用过程中的安全、权限问题。


### [6、服务降级底层是如何实现的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#6服务降级底层是如何实现的)  


Hystrix实现服务降级的功能是通过重写HystrixCommand中的getFallback()方法，当Hystrix的run方法或construct执行发生错误时转而执行getFallback()方法。


### [7、微服务的端到端测试意味着什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#7微服务的端到端测试意味着什么)  


端到端测试 验证工作流中的所有流程，以检查一切是否按预期工作。它还确保系统以统一的方式工作，从而满足业务需求。


### [8、spring cloud 断路器的作用是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#8spring-cloud-断路器的作用是什么)  


在分布式架构中，断路器模式的作用也是类似的，当某个服务单元发生故障（类似用电器发生短路）之后，通过断路器的故障监控（类似熔断保险丝），向调用方返回一个错误响应，而不是长时间的等待。这样就不会使得线程因调用故障服务被长时间占用不释放，避免了故障在分布式系统中的蔓延。


### [9、什么是端到端微服务测试？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#9什么是端到端微服务测试)  


端到端测试验证了工作流中的每个流程都正常运行。这可确保系统作为一个整体协同工作并满足所有要求。

通俗地说，你可以说端到端测试是一种测试，在特定时期后测试所有东西。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_17.png#alt=img%5C_17.png)

图14：测试层次 – 微服务面试问题


### [10、Spring Cloud Security](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新2021年面试题大汇总，附答案.md#10spring-cloud-security)  


安全工具包，对Zuul代理中的负载均衡OAuth2客户端及登录认证进行支持。


### 11、网关与过滤器有什么区别
### 12、在Spring MVC应用程序中使用WebMvcTest注释有什么用处？
### 13、微服务之间是如何独立通讯的
### 14、什么是Spring Cloud？
### 15、Ribbon底层实现原理
### 16、什么是断路器
### 17、分布式配置中心有那些框架？
### 18、分布式配置中心的作用？
### 19、为什么需要学习Spring Cloud
### 20、Eureka和ZooKeeper都可以提供服务注册与发现的功能,请说说两个的区别
### 21、什么是消费者驱动的合同（CDC）？
### 22、什么是幂等性?它是如何使用的？
### 23、微服务架构有哪些优势？
### 24、dubbo服务注册与发现原理
### 25、什么是持续监测？
### 26、@LoadBalanced注解的作用
### 27、什么是Spring Cloud？
### 28、Mock或Stub有什么区别？
### 29、您对Mike Cohn的测试金字塔了解多少？
### 30、SpringCloud限流：





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




