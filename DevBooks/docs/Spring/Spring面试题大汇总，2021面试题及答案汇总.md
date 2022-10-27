# Spring面试题大汇总，2022面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、如何使用SpringBoot实现异常处理？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#1如何使用springboot实现异常处理)  


Spring提供了一种使用ControllerAdvice处理异常的非常有用的方法。 我们通过实现一个ControlerAdvice类，来处理控制器类抛出的所有异常。


### [2、如何在SpringBoot中禁用Actuator端点安全性？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#2如何在springboot中禁用actuator端点安全性)  


默认情况下，所有敏感的HTTP端点都是安全的，只有具有ACTUATOR角色的用户才能访问它们。

安全性是使用标准的HttpServletRequest.isUserInRole方法实施的。 我们可以使用management.security.enabled = false 来禁用安全性。只有在执行机构端点在防火墙后访问时，才建议禁用安全性。

如何在自定义端口上运行SpringBoot应用程序？ 为了在自定义端口上运行SpringBoot应用程序，您可以在application.properties中指定端口。 server.port = 8090


### [3、谈一下领域驱动设计](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#3谈一下领域驱动设计)  


主要关注核心领域逻辑。基于领域的模型检测复杂设计。这涉及与公司层面领域方面的专家定期合作，以解决与领域相关的问题并改进应用程序的模型。在回答这个微服务面试问题时，您还需要提及DDD的核心基础知识。他们是：

**1、** DDD主要关注领域逻辑和领域本身。

**2、** 复杂的设计完全基于领域的模型。

**3、** 为了改进模型的设计并解决任何新出现的问题，DDD不断与公司领域方面的专家合作。


### [4、什么是 Apache Kafka？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#4什么是-apache-kafka)  


Apache Kafka 是一个分布式发布 - 订阅消息系统。它是一个可扩展的，容错的发布 - 订阅消息系统，它使我们能够构建分布式应用程序。这是一个 Apache 顶级项目。Kafka 适合离线和在线消息消费。


### [5、Spring Cloud Sleuth](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#5spring-cloud-sleuth)  


Spring Cloud应用程序的分布式请求链路跟踪，支持使用Zipkin、HTrace和基于日志（例如ELK）的跟踪。


### [6、Eureka和ZooKeeper都可以提供服务注册与发现的功能,请说说两个的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#6eureka和zookeeper都可以提供服务注册与发现的功能,请说说两个的区别)  


ZooKeeper保证的是CP,Eureka保证的是AP，ZooKeeper在选举期间注册服务瘫痪,虽然服务最终会恢复,但是选举期间不可用的。Eureka各个节点是平等关系,只要有一台Eureka就可以保证服务可用,而查询到的数据并不是最新的自我保护机制会导致Eureka不再从注册列表移除因长时间没收到心跳而应该过期的服务。Eureka仍然能够接受新服务的注册和查询请求,但是不会被同步到其他节点(高可用)。当网络稳定时,当前实例新的注册信息会被同步到其他节点中(最终一致性)。Eureka可以很好的应对因网络故障导致部分节点失去联系的情况,而不会像ZooKeeper一样使得整个注册系统瘫痪。

**1、** ZooKeeper有Leader和Follower角色,Eureka各个节点平等

**2、** ZooKeeper采用过半数存活原则,Eureka采用自我保护机制解决分区问题

**3、** Eureka本质上是一个工程,而ZooKeeper只是一个进程


### [7、Spring Cloud抛弃了Dubbo 的RPC通信，采用的是基于HTTP的REST方式。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#7spring-cloud抛弃了dubbo-的rpc通信采用的是基于http的rest方式。)  


严格来说，这两种方式各有优劣。虽然在一定程度上来说，后者牺牲了服务调用的性能，但也避免了上面提到的原生RPC带来的问题。而且REST相比RPC更为灵活，服务提供方和调用方的依赖只依靠一纸契约，不存在代码级别的强依赖，这在强调快速演化的微服务环境下，显得更为合适。



### [8、什么是 JavaConfig？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#8什么是-javaconfig)  


**1、** `面向对象的配置`。由于配置被定义为 JavaConfig 中的类，因此用户可以充分利用 Java 中的面向对象功能。一个配置类可以继承另一个，重写它的[@Bean ](/Bean ) 方法等。

**2、** `减少或消除 XML 配置`。基于依赖注入原则的外化配置的好处已被证明。但是，许多开发人员不希望在 XML 和 Java 之间来回切换。JavaConfig 为开发人员提供了一种纯 Java 方法来配置与 XML 配置概念相似的 Spring 容器。从技术角度来讲，只使用 JavaConfig 配置类来配置容器是可行的，但实际上很多人认为将JavaConfig 与 XML 混合匹配是理想的。

**3、** `类型安全和重构友好`。JavaConfig 提供了一种类型安全的方法来配置 Spring容器。由于 Java 5.0 对泛型的支持，现在可以按类型而不是按名称检索 bean，不需要任何强制转换或基于字符串的查找。


### [9、使用Spring框架的好处是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#9使用spring框架的好处是什么)  


**轻量：**Spring 是轻量的，基本的版本大约2MB。

控制反转：Spring通过控制反转实现了松散耦合，对象们给出它们的依赖，而不是创建或查找依赖的对象们。

面向切面的编程(AOP)：Spring支持面向切面的编程，并且把应用业务逻辑和系统服务分开。

**容器：**Spring 包含并管理应用中对象的生命周期和配置。

**MVC框架：**Spring的WEB框架是个精心设计的框架，是Web框架的一个很好的替代品。

**事务管理：**Spring 提供一个持续的事务管理接口，可以扩展到上至本地事务下至全局事务（JTA）。

**异常处理：**Spring 提供方便的API把具体技术相关的异常（比如由JDBC，Hibernate or JDO抛出的）转化为一致的unchecked 异常。


### [10、SpringBoot 提供了哪些核心功能？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021面试题及答案汇总.md#10springboot-提供了哪些核心功能)  


**1、** 独立运行 Spring 项目

**2、** 内嵌 Servlet 容器

SpringBoot 可以选择内嵌 Tomcat、Jetty 或者 Undertow，这样我们无须以 war 包形式部署项目。

**3、** 提供 Starter 简化 Maven 配置

例如，当你使用了 spring-boot-starter-web ，会自动加入如下依赖：`spring-boot-starter-web` 的 pom 文件

**4、** 自动配置 Spring Bean

SpringBoot 检测到特定类的存在，就会针对这个应用做一定的配置，进行自动配置 Bean ，这样会极大地减少我们要使用的配置。

**5、** 准生产的应用监控

SpringBoot 提供基于 HTTP、JMX、SSH 对运行时的项目进行监控。

**6、** 无代码生成和 XML 配置

SpringBoot 没有引入任何形式的代码生成，它是使用的 Spring 4.0 的条件 [@Condition ](/Condition ) 注解以实现根据条件进行配置。同时使用了 Maven /Gradle 的依赖传递解析机制来实现 Spring 应用里面的自动配置。


### 11、什么是 AOP 切点
### 12、什么是 Spring Data REST?
### 13、什么是金丝雀释放？
### 14、第⼆层缓存：
### 15、列举 IoC 的一些好处。
### 16、合同测试你懂什么？
### 17、YAML 配置的优势在哪里 ?
### 18、比较一下 Spring Security 和 Shiro 各自的优缺点 ?
### 19、可以在SpringBoot application中禁用默认的Web服务器吗？
### 20、如何设计一套API接口
### 21、微服务之间是如何独立通讯的?
### 22、怎样开启注解装配？
### 23、eureka缓存机制：
### 24、Spring Cloud Sleuth
### 25、spring JDBC API 中存在哪些类？
### 26、Spring MVC的控制器是不是单例模式,如果是,有什么问题,怎么解决？
### 27、自动装配有什么局限？
### 28、eureka和zookeeper都可以提供服务注册与发现的功能，请说说两个的区别？
### 29、是否可以在SpringBoot中覆盖或替换嵌入式Tomcat？
### 30、spring 中有多少种 IOC 容器？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




