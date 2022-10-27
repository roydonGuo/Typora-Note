# Spring面试题大全带答案，持续更新


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、SpringBoot 的自动配置是如何实现的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#1springboot-的自动配置是如何实现的)  


SpringBoot 项目的启动注解是：@SpringBootApplication，其实它就是由下面三个注解组成的：

**1、** [@Configuration ](/Configuration )

**2、** [@ComponentScan ](/ComponentScan )

**3、** @EnableAutoConfiguration

其中 @EnableAutoConfiguration 是实现自动配置的入口，该注解又通过 [@Import ](/Import ) 注解导入了AutoConfigurationImportSelector，在该类中加载 META-INF/spring.factories 的配置信息。然后筛选出以 EnableAutoConfiguration 为 key 的数据，加载到 IOC 容器中，实现自动配置功能！


### [2、能否举一个例子来解释更多 Staters 的内容？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#2能否举一个例子来解释更多-staters-的内容)  


让我们来思考一个 Stater 的例子 -SpringBoot Stater Web。

如果你想开发一个 web 应用程序或者是公开 REST 服务的应用程序。SpringBoot Start Web 是首选。让我们使用 Spring Initializr 创建一个 SpringBoot Start Web 的快速项目。

**依赖项可以被分为：**

**1、** Spring - core，beans，context，aop

**2、** Web MVC - （Spring MVC）

**3、** Jackson - for JSON Binding

**4、** Validation - Hibernate,Validation API

**5、** Enbedded Servlet Container - Tomcat

**6、** Logging - logback,slf4j

任何经典的 Web 应用程序都会使用所有这些依赖项。SpringBoot Starter Web 预先打包了这些依赖项。

作为一个开发者，我不需要再担心这些依赖项和它们的兼容版本。


### [3、什么是Spring Cloud Gateway?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#3什么是spring-cloud-gateway)  


Spring Cloud Gateway是Spring Cloud官方推出的第二代网关框架，取代Zuul网关。网关作为流量的，在微服务系统中有着非常作用，网关常见的功能有路由转发、权限校验、限流控制等作用。

使用了一个RouteLocatorBuilder的bean去创建路由，除了创建路由RouteLocatorBuilder可以让你添加各种predicates和filters，predicates断言的意思，顾名思义就是根据具体的请求的规则，由具体的route去处理，filters是各种过滤器，用来对请求做各种判断和修改。


### [4、当 SpringBoot 应用程序作为 Java 应用程序运行时，后台会发生什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#4当-springboot-应用程序作为-java-应用程序运行时后台会发生什么)  


如果你使用 Eclipse IDE，Eclipse maven 插件确保依赖项或者类文件的改变一经添加，就会被编译并在目标文件中准备好！在这之后，就和其它的 Java 应用程序一样了。

当你启动 java 应用程序的时候，spring boot 自动配置文件就会魔法般的启用了。

当 SpringBoot 应用程序检测到你正在开发一个 web 应用程序的时候，它就会启动 tomcat。


### [5、我们如何监视所有 SpringBoot 微服务？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#5我们如何监视所有-springboot-微服务)  


SpringBoot 提供监视器端点以监控各个微服务的度量。这些端点对于获取有关应用程序的信息（如它们是否已启动）以及它们的组件（如数据库等）是否正常运行很有帮助。但是，使用监视器的一个主要缺点或困难是，我们必须单独打开应用程序的知识点以了解其状态或健康状况。想象一下涉及 50 个应用程序的微服务，管理员将不得不击中所有 50 个应用程序的执行终端。为了帮助我们处理这种情况，我们将使用位于的开源项目。它建立在 SpringBoot Actuator 之上，它提供了一个 Web UI，使我们能够可视化多个应用程序的度量。


### [6、什么是嵌入式服务器？我们为什么要使用嵌入式服务器呢?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#6什么是嵌入式服务器我们为什么要使用嵌入式服务器呢)  


思考一下在你的虚拟机上部署应用程序需要些什么。

第一步：安装 Java

第二部：安装 Web 或者是应用程序的服务器（Tomat/Wbesphere/Weblogic 等等）

第三部：部署应用程序 war 包

如果我们想简化这些步骤，应该如何做呢？

让我们来思考如何使服务器成为应用程序的一部分？

你只需要一个安装了 Java 的虚拟机，就可以直接在上面部署应用程序了，

是不是很爽？

这个想法是嵌入式服务器的起源。

当我们创建一个可以部署的应用程序的时候，我们将会把服务器（例如，tomcat）嵌入到可部署的服务器中。

例如，对于一个 SpringBoot 应用程序来说，你可以生成一个包含 Embedded Tomcat 的应用程序 jar。你就可以像运行正常 Java 应用程序一样来运行 web 应用程序了。

嵌入式服务器就是我们的可执行单元包含服务器的二进制文件（例如，tomcat.jar）。


### [7、注解原理是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#7注解原理是什么)  


注解本质是一个继承了Annotation的特殊接口，其具体实现类是Java运行时生成的动态代理类。我们通过反射获取注解时，返回的是Java运行时生成的动态代理对象。通过代理对象调用自定义注解的方法，会最终调用AnnotationInvocationHandler的invoke方法。该方法会从memberValues这个Map中索引出对应的值。而memberValues的来源是Java常量池。


### [8、Spring Cloud Consul](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#8spring-cloud-consul)  


基于Hashicorp Consul的服务治理组件。


### [9、介绍一下 WebApplicationContext](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#9介绍一下-webapplicationcontext)  


WebApplicationContext 继承了ApplicationContext 并增加了一些WEB应用必备的特有功能，它不同于一般的ApplicationContext ，因为它能处理主题，并找到被关联的servlet。




### [10、如何理解 Spring 中的代理？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大全带答案，持续更新.md#10如何理解-spring-中的代理)  


将 Advice 应用于目标对象后创建的对象称为代理。在客户端对象的情况下，目标对象和代理对象是相同的。

```
Advice + Target Object = Proxy
```


### 11、您将如何在微服务上执行安全测试？
### 12、什么是微服务架构
### 13、Spring MVC中函数的返回值是什么？
### 14、Spring Framework 有哪些不同的功能？
### 15、BeanFactory – BeanFactory 实现举例。
### 16、什么是YAML？
### 17、spring boot监听器流程?
### 18、什么是 AOP什么是引入?
### 19、如何在 SpringBoot 启动的时候运行一些特定的代码？
### 20、spring boot 核心配置文件是什么？bootstrap、properties 和 application、properties 有何区别 ?
### 21、什么是 SpringBoot Stater ？
### 22、SpringBoot 自动配置原理
### 23、什么是Semantic监控？
### 24、什么是Spring MVC？简单介绍下你对Spring MVC的理解？
### 25、微服务测试的主要障碍是什么？
### 26、如何重新加载SpringBoot上的更改，而无需重新启动服务器？
### 27、Spring MVC常用的注解有哪些？
### 28、SpringBoot默认支持的日志框架有哪些？可以进行哪些设置？
### 29、[@RequestMapping ](/RequestMapping ) 注解有什么用？
### 30、22。你能否给出关于休息和微服务的要点？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




