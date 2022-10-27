# Spring最新面试题，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、自动装配有哪些局限性 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#1自动装配有哪些局限性-)  


**自动装配的局限性是：**

重写： 你仍需用 和  配置来定义依赖，意味着总要重写自动装配。

基本数据类型：你不能自动装配简单的属性，如基本数据类型，String字符串，和类。

模糊特性：自动装配不如显式装配精确，如果有可能，建议使用显式装配。


### [2、什么是 AOP 目标对象?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#2什么是-aop-目标对象)  


被一个或者多个切面所通知的对象。它通常是一个代理对象。也指被通知（advised）对象。


### [3、shiro和oauth还有cas他们之间的关系是什么？问下您公司权限是如何设计，还有就是这几个概念的区别。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#3shiro和oauth还有cas他们之间的关系是什么问下您公司权限是如何设计还有就是这几个概念的区别。)  


cas和oauth是一个解决单点登录的组件，shiro主要是负责权限安全方面的工作，所以功能点不一致。但往往需要单点登陆和权限控制一起来使用，所以就有 cas+shiro或者oauth+shiro这样的组合。

token一般是客户端登录后服务端生成的令牌，每次访问服务端会进行校验，一般保存到内存即可，也可以放到其他介质；Redis可以做Session共享，如果前端web服务器有几台负载，但是需要保持用户登录的状态，这场景使用比较常见。

我们公司使用oauth+shiro这样的方式来做后台权限的管理，oauth负责多后台统一登录认证，shiro负责给登录用户赋予不同的访问权限。


### [4、什么是Spring Cloud？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#4什么是spring-cloud)  


在微服务中，SpringCloud是一个提供与外部系统集成的系统。它是一个敏捷的框架，可以短平快构建应用程序。与有限数量的数据处理相关联，它在微服务体系结构中起着非常重要的作用。 **以下为 Spring Cloud 的核心特性**：

**1、** 版本化/分布式配置。

**2、** 服务注册和发现。

**3、** 服务和服务之间的调用。

**4、** 路由。

**5、** 断路器和负载平衡。

**6、** 分布式消息传递。


### [5、谈谈服务雪崩效应](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#5谈谈服务雪崩效应)  


雪崩效应是在大型互联网项目中，当某个服务发生宕机时，调用这个服务的其他服务也会发生宕机，大型项目的微服务之间的调用是互通的，这样就会将服务的不可用逐步扩大到各个其他服务中，从而使整个项目的服务宕机崩溃.发生雪崩效应的原因有以下几点

单个服务的代码存在bug、2请求访问量激增导致服务发生崩溃(如大型商城的枪红包，秒杀功能)、3.服务器的硬件故障也会导致部分服务不可用.


### [6、ApplicationContext通常的实现是什么?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#6applicationcontext通常的实现是什么)  


**1、** FileSystemXmlApplicationContext ：此容器从一个XML文件中加载beans的定义，XML Bean 配置文件的全路径名必须提供给它的构造函数。

**2、** ClassPathXmlApplicationContext：此容器也从一个XML文件中加载beans的定义，这里，你需要正确设置classpath因为这个容器将在classpath里找bean配置。

**3、** WebXmlApplicationContext：此容器加载一个XML文件，此文件定义了一个WEB应用的所有bean。


### [7、网关的作用是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#7网关的作用是什么)  


统一管理微服务请求，权限控制、负载均衡、路由转发、监控、安全控制黑名单和白名单等


### [8、什么是Spring Profiles？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#8什么是spring-profiles)  


Spring Profiles允许用户根据配置文件（dev，test，prod等）来注册bean。因此，当应用程序在开发中运行时，只有某些bean可以加载，而在PRODUCTION中，某些其他bean可以加载。假设我们的要求是Swagger文档仅适用于QA环境，并且禁用所有其他文档。这可以使用配置文件来完成。SpringBoot使得使用配置文件非常简单。


### [9、[@Required ](/Required ) 注解](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#9[@required-]/required--注解)  


这个注解表明bean的属性必须在配置的时候设置，通过一个bean定义的显式的属性值或通过自动装配，若@Required注解的bean属性未被设置，容器将抛出BeanInitializationException。


### [10、我们如何监视所有 SpringBoot 微服务？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，常见面试题及答案汇总.md#10我们如何监视所有-springboot-微服务)  


SpringBoot 提供监视器端点以监控各个微服务的度量。这些端点对于获取有关应用程序的信息（如它们是否已启动）以及它们的组件（如数据库等）是否正常运行很有帮助。但是，使用监视器的一个主要缺点或困难是，我们必须单独打开应用程序的知识点以了解其状态或健康状况。想象一下涉及 50 个应用程序的微服务，管理员将不得不击中所有 50 个应用程序的执行终端。为了帮助我们处理这种情况，我们将使用位于的开源项目。 它建立在 SpringBoot Actuator 之上，它提供了一个 Web UI，使我们能够可视化多个应用程序的度量。


### 11、如何在 spring 中启动注解装配？
### 12、什么是服务熔断
### 13、Springboot 有哪些优点？
### 14、如果想在拦截的方法里面得到从前台传入的参数,怎么得到？
### 15、微服务同时调用多个接口，怎么支持事务的啊？
### 16、访问RESTful微服务的方法是什么？
### 17、SpringBoot 有哪些优点？
### 18、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？
### 19、SpringBoot 常用的 Starter 有哪些？
### 20、SOA和微服务架构之间的主要区别是什么？
### 21、springcloud和dubbo有哪些区别
### 22、什么是 spring bean？
### 23、[@Autowired ](/Autowired ) 注解
### 24、Spring Cloud Consul
### 25、SpringCloud由什么组成
### 26、什么是依赖注入？
### 27、SpringBoot的启动器有哪几种?
### 28、什么是Apache Kafka？
### 29、Spring Cloud Bus
### 30、Spring Cloud和各子项目版本对应关系
### 31、SpringBoot自动配置的原理





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




