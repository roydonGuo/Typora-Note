# Spring高级面试题及答案，最新版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是Spring Batch？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#1什么是spring-batch)  


SpringBoot Batch提供可重用的函数，这些函数在处理大量记录时非常重要，包括日志/跟踪，事务管理，作业处理统计信息，作业重新启动，跳过和资源管理。它还提供了更先进的技术服务和功能，通过优化和分区技术，可以实现极高批量和高性能批处理作业。简单以及复杂的大批量批处理作业可以高度可扩展的方式利用框架处理重要大量的信息。


### [2、spring DAO 有什么用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#2spring-dao-有什么用)  


Spring DAO 使得 JDBC，Hibernate 或 JDO 这样的数据访问技术更容易以一种统一的方式工作。 这使得用户容易在持久性技术之间切换。 它还允许您在编写代码时，无需考虑捕获每种技术不同的异常。


### [3、什么是 YAML？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#3什么是-yaml)  


YAML 是一种人类可读的数据序列化语言。它通常用于配置文件。与属性文件相比，如果我们想要在配置文件中添加复杂的属性，YAML 文件就更加结构化，而且更少混淆。可以看出 YAML 具有分层配置数据。


### [4、使⽤中碰到的坑](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#4使⽤中碰到的坑)  


**1、** 超时：确保Hystrix超时时间配置为⻓于配置的Ribbon超时时间

**2、** feign path：feign客户端在部署时若有contextpath应该设置 path="/***"来匹配你的服务名。

**3、** 版本：SpringBoot和springcloud版本要兼容。


### [5、什么是 AOP 通知](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#5什么是-aop-通知)  


通知是个在方法执行前或执行后要做的动作，实际上是程序执行时要通过SpringAOP框架触发的代码段。

Spring切面可以应用五种类型的通知：

**1、** before：前置通知，在一个方法执行前被调用。

**2、** after: 在方法执行之后调用的通知，无论方法执行是否成功。

**3、** after-returning: 仅当方法成功完成后执行的通知。

**4、** after-throwing: 在方法抛出异常退出时执行的通知。

**5、** around: 在方法执行之前和之后调用的通知。


### [6、列举 IoC 的一些好处](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#6列举-ioc-的一些好处)  


**1、** IoC 的一些好处是：

**2、** 它将最小化应用程序中的代码量。

**3、** 它将使您的应用程序易于测试，因为它不需要单元测试用例中的任何单例或 JNDI 查找机制。

**4、** 它以最小的影响和最少的侵入机制促进松耦合。

**5、** 它支持即时的实例化和延迟加载服务。


### [7、SpringBoot中的监视器是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#7springboot中的监视器是什么)  


Spring boot actuator是spring启动框架中的重要功能之一。Spring boot监视器可帮助您访问生产环境中正在运行的应用程序的当前状态。有几个指标必须在生产环境中进行检查和监控。即使一些外部应用程序可能正在使用这些服务来向相关人员触发警报消息。监视器模块公开了一组可直接作为HTTP URL访问的REST端点来检查状态。


### [8、SpringBoot 中的监视器是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#8springboot-中的监视器是什么)  


Spring boot actuator 是 spring 启动框架中的重要功能之一。Spring boot 监视器可帮助您访问生产环境中正在运行的应用程序的当前状态。有几个指标必须在生产环境中进行检查和监控。即使一些外部应用程序可能正在使用这些服务来向相关人员触发警报消息。监视器模块公开了一组可直接作为 HTTP URL 访问的REST 端点来检查状态。


### [9、Spring MVC里面拦截器是怎么写的](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#9spring-mvc里面拦截器是怎么写的)  


有两种写法,一种是实现HandlerInterceptor接口，另外一种是继承适配器类，接着在接口方法当中，实现处理逻辑；然后在Spring MVC的配置文件中配置拦截器即可：

```
<!-- 配置Spring MVC的拦截器 -->
< mvc: interceptors >
<!-- 配置一个拦截器的Bean就可以了 默认是对所有请求都拦截 -->
< bean id = "myInterceptor"
class = "com.zwp.action.MyHandlerInterceptor" > < /bean>
<!-- 只针对部分请求拦截 -->
<mvc:interceptor>
   <mvc:mapping path="/modelMap.do " />
   <bean class="
com.
zwp.action.MyHandlerInterceptorAdapter " />
</mvc:interceptor>
</mvc:interceptors>
```


### [10、Spring Cache 三种常用的缓存注解和意义？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，最新版.md#10spring-cache-三种常用的缓存注解和意义)  


**1、** [@Cacheable ](/Cacheable ) ，用来声明方法是可缓存，将结果存储到缓存中以便后续使用相同参数调用时不需执行实际的方法，直接从缓存中取值。

**2、** @CachePut，使用 [@CachePut ](/CachePut ) 标注的方法在执行前，不会去检查缓存中是否存在之前执行过的结果，而是每次都会执行该方法，并将执行结果以键值对的形式存入指定的缓存中。

**3、** @CacheEvict，是用来标注在需要清除缓存元素的方法或类上的，当标记在一个类上时表示其中所有的方法的执行都会触发缓存的清除操作。


### 11、SpringBoot有哪些优点？
### 12、什么是 Spring Batch？
### 13、什么是Idempotence以及它在哪里使用？
### 14、SpringBoot自动配置的原理是什么？
### 15、什么是基于注解的容器配置
### 16、@Controller注解的作用
### 17、SpringBoot 怎么用好自动配置，精髓:
### 18、什么是耦合和凝聚力？
### 19、有哪些类型的通知（Advice）？
### 20、AOP 有哪些实现方式？
### 21、微服务架构的优缺点是什么？
### 22、您使用了哪些starter maven依赖项？
### 23、如何集成SpringBoot和ActiveMQ？
### 24、第⼀层缓存：
### 25、如何通过HibernateDaoSupport将Spring和Hibernate结合起来？
### 26、JPA 和 Hibernate 有哪些区别？JPA 可以支持动态 SQL 吗？
### 27、微服务的缺点：
### 28、Spring由哪些模块组成?
### 29、@RequestMapping注解的作用
### 30、Spring Cloud Zookeeper





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




