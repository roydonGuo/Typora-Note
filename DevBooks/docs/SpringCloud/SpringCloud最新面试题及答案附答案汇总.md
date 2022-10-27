# SpringCloud最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、为什么人们会犹豫使用微服务？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#1为什么人们会犹豫使用微服务)  


我见过许多开发者在这个问题上摸索。毕竟，在面试微服务架构师角色时，他们会被问到这个问题，所以承认它的缺点可能有点棘手。以下是一些很好的答案：

它们需要大量协作 - 微服务需要大量的合作。不同的微服务模块，可能分散在不同的团队，团队之间需要始终保持良好的同步。

他们需要建立繁重的架构 - 系统是分布式的，架构涉及很多。 他们需要过多的计划来处理操作开销 - 如果您计划使用微服务架构，则需要为操作开销做好准备。 需要熟练的专业人员，他们可以支持异构分布的微服务。


### [2、Spring Cloud 是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#2spring-cloud-是什么)  


**1、** Spring Cloud是一系列框架的有序集合。它利用SpringBoot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、智能路由、消息总线、负载均衡、断路器、数据监控等，都可以用SpringBoot的开发风格做到一键启动和部署。

**2、** Spring Cloud并没有重复制造轮子，它只是将各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过SpringBoot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包。


### [3、为什么需要域驱动设计（DDD）？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#3为什么需要域驱动设计ddd)  


![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_11.png#alt=img%5C_11.png)

图9：我们需要DDD的因素 – 微服务面试问题


### [4、Spring Cloud和SpringBoot版本对应关系](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#4spring-cloud和springboot版本对应关系)  

| Spring Cloud Version | SpringBoot Version |
| --- | --- |
| Hoxton | 2.2.x |
| Greenwich | 2.1.x |
| Finchley | 2.0.x |
| Edgware | 1.5.x |
| Dalston |  |



### [5、Spring Cloud抛弃了Dubbo 的RPC通信，采用的是基于HTTP的REST方式。](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#5spring-cloud抛弃了dubbo-的rpc通信采用的是基于http的rest方式。)  


严格来说，这两种方式各有优劣。虽然在一定程度上来说，后者牺牲了服务调用的性能，但也避免了上面提到的原生RPC带来的问题。而且REST相比RPC更为灵活，服务提供方和调用方的依赖只依靠一纸契约，不存在代码级别的强依赖，这在强调快速演化的微服务环境下，显得更为合适。



### [6、什么是SpringBoot？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#6什么是springboot)  


Spring boot是微服务面试问题的主要话题。 随着新功能的加入，Spring变得越来越复杂。无论何时启动新项目，都必须添加新的构建路径或Maven依赖项。简而言之，你需要从头开始做每件事。SpringBoot是一种帮助您避免所有代码配置的解决方案。


### [7、微服务有什么特点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#7微服务有什么特点)  


您可以列出微服务的特征，如下所示：

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_9.png#alt=img%5C_9.png)

图7：微服务的特征 – 微服务访谈问题


### [8、什么是Spring Cloud Bus?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#8什么是spring-cloud-bus)  


spring cloud bus 将分布式的节点用轻量的消息代理连接起来，它可以用于广播配置文件的更改或者服务直接的通讯，也可用于监控。

如果修改了配置文件，发送一次请求，所有的客户端便会重新读取配置文件。

**使用:**

**1、** 添加依赖

**2、** 配置rabbimq


### [9、SpringBoot和springcloud认识](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#9springboot和springcloud认识)  


**1、** SpringBoot 是 Spring 的⼀套快速配置脚⼿架，可以基于SpringBoot 快速开发单个微服务，Spring Cloud是⼀个基于SpringBoot实现的云应⽤开发⼯具；

**2、** SpringBoot专注于快速、⽅便集成的单个微服务个体，Spring Cloud关注全局的服务治理框架；

**3、** SpringBoot使⽤了默认⼤于配置的理念，很多集成⽅案已经帮你选择好了，能不配置就不配置；

**4、** Spring Cloud很⼤的⼀部分是基于SpringBoot来实现，可以不基于SpringBoot吗？不可以。


### [10、链路跟踪Sleuth](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题及答案附答案汇总.md#10链路跟踪sleuth)  


当我们项目中引入Spring Cloud Sleuth后，每次链路请求都会添加一串追踪信息，格式是[server-name, main-traceId,sub-spanId,boolean]：

**1、** server-name：服务结点名称。

**2、** main-traceId：一条链路唯一的ID，为TraceID。

**3、** sub-spanId：链路中每一环的ID，为SpanID。

**4、** boolean：是否将信息输出到Zipkin等服务收集和展示。

Sleuth的实现是基于HTTP的，为了在数据的收集过程中不能影响到正常业务，Sleuth会在每个请求的Header上添加跟踪需求的重要信息。这样在数据收集时，只需要将Header上的相关信息发送给对应的图像工具即可，图像工具根据上传的数据，按照Span对应的逻辑进行分析、展示。



### 11、PACT在微服务架构中的用途是什么？
### 12、如何配置SpringBoot应用程序日志记录？
### 13、我们如何进行跨功能测试？
### 14、REST 和RPC对比
### 15、什么是金丝雀释放？
### 16、双因素身份验证的凭据类型有哪些？
### 17、Container在微服务中的用途是什么？
### 18、Spring Cloud Security
### 19、eureka缓存机制：
### 20、谈谈服务雪崩效应
### 21、什么是无所不在的语言？
### 22、第⼀层缓存：
### 23、SOA和微服务架构之间的主要区别是什么？
### 24、微服务设计的基础是什么？
### 25、康威定律是什么？
### 26、合同测试你懂什么？
### 27、第⼆层缓存：
### 28、服务雪崩效应产生的原因
### 29、Spring Cloud解决了哪些问题？
### 30、康威定律是什么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




