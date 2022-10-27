# Spring最新基础面试题及答案整理


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、为什么我们不建议在实际的应用程序中使用 Spring Data Rest?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#1为什么我们不建议在实际的应用程序中使用-spring-data-rest)  


我们认为 Spring Data Rest 很适合快速原型制造！在大型应用程序中使用需要谨慎。

通过 Spring Data REST 你可以把你的数据实体作为 RESTful 服务直接。

当你设计 RESTful 服务器的时候，最佳实践表明，你的接口应该考虑到两件重要的事情：

你的模型范围。

你的客户。

通过 With Spring Data REST，你不需要再考虑这两个方面，只需要作为 TEST 服务实体。

这就是为什么我们建议使用 Spring Data Rest 在快速原型构造上面，或者作为项目的初始解决方法。对于完整演变项目来说，这并不是一个好的注意。


### [2、Ribbon是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#2ribbon是什么)  


**1、** Ribbon是Netflix发布的开源项目，主要功能是提供客户端的软件负载均衡算法

**2、** Ribbon客户端组件提供一系列完善的配置项，如连接超时，重试等。简单的说，就是在配置文件中列出后面所有的机器，Ribbon会自动的帮助你基于某种规则（如简单轮询，随即连接等）去连接这些机器。我们也很容易使用Ribbon实现自定义的负载均衡算法。（有点类似Nginx）


### [3、如何禁用特定的自动配置类？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#3如何禁用特定的自动配置类)  


若发现任何不愿使用的特定自动配置类，可以使用@EnableAutoConfiguration的排除属性。

//By using "exclude"

@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})

另一方面，如果类别不在类路径上，则可以使用excludeName类注解，并且指定完全限定名。

//By using "excludeName"

@EnableAutoConfiguration(excludeName={Foo.class})

此外，SpringBoot还具有控制排除自动配置类列表的功能，可以通过使用spring.autoconfigure.exclude property来实现。可以将其添加到 propertie应用程序中，并且可以添加逗号分隔的多个类。

//By using property file

spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration


### [4、自动装配有哪些方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#4自动装配有哪些方式)  


Spring 容器能够自动装配 bean。也就是说，可以通过检查 BeanFactory 的内容让 Spring 自动解析 bean 的协作者。

自动装配的不同模式：

**1、** 这是默认设置，表示没有自动装配。应使用显式 bean 引用进行装配。byName

**2、** 它根据 bean 的名称注入对象依赖项。它匹配并装配其属性与 XML 文件中由相同名称定义的 bean。byType

**3、** 它根据类型注入对象依赖项。如果属性的类型与 XML 文件中的一个 bean 名称匹配，则匹配并装配属性。构造函数

**4、** 它通过调用类的构造函数来注入依赖项。它有大量的参数。autodetect

**5、** 首先容器尝试通过构造函数使用 autowire 装配，如果不能，则尝试通过 byType 自动装配。


### [5、spring 支持集中 bean scope？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#5spring-支持集中-bean-scope)  


**Spring bean 支持 5 种 scope：**

**1、** Singleton - 每个 Spring IoC 容器仅有一个单实例。

**2、** Prototype - 每次请求都会产生一个新的实例。

**3、** Request - 每一次 HTTP 请求都会产生一个新的实例，并且该 bean 仅在当前 HTTP 请求内有效。

**4、** Session - 每一次 HTTP 请求都会产生一个新的 bean，同时该 bean 仅在当前 HTTP session 内有效。

**5、** Global-session - 类似于标准的 HTTP Session 作用域，不过它仅仅在基于 portlet 的 web 应用中才有意义。 Portlet 规范定义了全局 Session 的概念，它被所有构成某个 portlet web 应用的各种不同的 portlet 所共享。 在 global session 作用域中定义的 bean 被限定于全局 portlet Session 的生命周期范围内。 如果你在 web 中使用 global session 作用域来标识 bean，那么 web 会自动当成 session 类型来使用。

**6、** 仅当用户使用支持 Web 的 ApplicationContext 时，最后三个才可用。


### [6、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#6springboot-的核心注解是哪个它主要由哪几个注解组成的)  


启动类上面的注解是@SpringBootApplication，它也是 SpringBoot 的核心注解，主要组合包含了以下 3 个注解：

@SpringBootConfiguration：组合了 [@Configuration ](/Configuration ) 注解，实现配置文件的功能。

@EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项， 例如：`java 如关闭数据源自动配置功能： @SpringBootApplication(exclude = { DataSourceAutoConfiguration、class })。`

@ComponentScan：Spring组件扫描。


### [7、什么是 Spring Framework？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#7什么是-spring-framework)  


**1、** Spring 是一个开源应用框架，旨在降低应用程序开发的复杂度。

**2、** 它是轻量级、松散耦合的。

**3、** 它具有分层体系结构，允许用户选择组件，同时还为 J2EE 应用程序开发提供了一个有凝聚力的框架。

**4、** 它可以集成其他框架，如 Structs、Hibernate、EJB 等，所以又称为框架的框架。


### [8、如何不通过任何配置来选择 Hibernate 作为 JPA 的默认实现？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#8如何不通过任何配置来选择-hibernate-作为-jpa-的默认实现)  


因为 SpringBoot 是自动配置的。

**下面是我们添加的依赖项:**

spring-boot-stater-data-jpa 对于 Hibernate 和 JPA 有过渡依赖性。

当 SpringBoot 在类路径中检测到 Hibernate 中，将会自动配置它为默认的 JPA 实现。


### [9、Spring由哪些模块组成?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#9spring由哪些模块组成)  


**以下是Spring 框架的基本模块：**

**1、** Core module

**2、** Bean module

**3、** Context module

**4、** Expression Language module

**5、** JDBC module

**6、** ORM module

**7、** OXM module

**8、** Java Messaging Service(JMS) module

**9、** Transaction module

**10、** Web module

**11、** Web-Servlet module

**12、** Web-Struts module

**13、** Web-Portlet module


### [10、什么是双因素身份验证？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新基础面试题及答案整理.md#10什么是双因素身份验证)  


双因素身份验证为帐户登录过程启用第二级身份验证。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_14.png#alt=img%5C_14.png)

图11： 双因素认证的表示 – 微服务访谈问题

因此，假设用户必须只输入用户名和密码，那么这被认为是单因素身份验证。


### 11、SpringBoot 可以兼容老 Spring 项目吗，如何做？
### 12、什么是DispatcherServlet
### 13、SpringBoot如何配置log4j？
### 14、spring 支持哪些 ORM 框架
### 15、Spring Cloud Task
### 16、什么是 spring 的内部 bean？
### 17、什么是 AOP 连接点
### 18、Mock或Stub有什么区别？
### 19、什么是feigin？它的优点是什么？
### 20、解释基于注解的切面实现
### 21、你如何理解 SpringBoot 配置加载顺序？
### 22、SpringBoot 打成的 jar 和普通的 jar 有什么区别 ?
### 23、Spring Cloud Zookeeper
### 24、什么是织入。什么是织入应用的不同点？
### 25、如何覆盖SpringBoot项目的默认属性？
### 26、我们如何监视所有SpringBoot微服务？
### 27、什么是SpringBoot？
### 28、服务雪崩效应产生的原因
### 29、使用Spring通过什么方式访问Hibernate?
### 30、如何使用SpringBoot实现分页和排序？
### 31、SpringBoot 2.X 有什么新特性？与 1.X 有什么区别？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




