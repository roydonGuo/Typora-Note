# SpringBoot最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、spring boot 核心的两个配置文件：](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#1spring-boot-核心的两个配置文件：)  


**1、** bootstrap (.yml 或.properties)：boostrap 由父 ApplicationContext 加载的，比 applicaton 优先加载，配置在应用程序上下文的引导阶段生效。一般来说我们在 Spring Cloud Config 或者 Nacos 中会用到它。且 boostrap 里面的属性不能被覆盖；

**2、** application (. yml 或者 . properties)：由ApplicatonContext 加载，用于 spring boot 项目的自动化配置。


### [2、是否可以在Spring boot中更改嵌入式Tomcat服务器的端口?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#2是否可以在spring-boot中更改嵌入式tomcat服务器的端口)  


是的，更改端口是可行的。可以使用application.properties文件更改端口。但需要提到“server.port”（即server.port=8081）。确保项目类路径中有application.properties；后续工作将由REST Spring框架接手。如果提到server.port=0，那么它将自动分配任何可用的端口。


### [3、如何在 SpringBoot 启动的时候运行一些特定的代码？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#3如何在-springboot-启动的时候运行一些特定的代码)  


可以实现接口 ApplicationRunner 或者 CommandLineRunner，这两个接口实现方式一样，它们都只提供了一个 run 方法


### [4、什么是 CSRF 攻击？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#4什么是-csrf-攻击)  


CSRF 代表跨站请求伪造。这是一种攻击，迫使最终用户在当前通过身份验证的Web 应用程序上执行不需要的操作。CSRF 攻击专门针对状态改变请求，而不是数据窃取，因为攻击者无法查看对伪造请求的响应。


### [5、bootstrap.yml和application.yml有什么区别?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#5bootstrapyml和applicationyml有什么区别)  


**1、** Spring Cloud 构建于 SpringBoot 之上，在 SpringBoot 中有两种上下文，一种是 bootstrap，另外一种是 application。

**2、** application 配置文件这个容易理解，主要用于 SpringBoot 项目的`自动化配置`。

**3、** bootstrap 是应用程序的父上下文，也就是说 `bootstrap 加载优先于 applicaton`。

**4、** bootstrap 主要用于从`额外的资源来加载配置信息`，还可以在本地外部配置文件中解密属性。

**5、** 这两个上下文`共用一个环境`，它是任何Spring应用程序的外部属性的来源。

**6、** bootstrap 里面的属性会`优先加载`，它们默认也不能被本地相同配置覆盖。

**7、** boostrap 由父 ApplicationContext 加载，`比 applicaton 优先加载`

**8、** boostrap 里面的属性`不能被覆盖`


### [6、SpringBoot的缺点](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#6springboot的缺点)  


我觉得是为难人，SpringBoot在目前我觉得没有什么缺点，非要找一个出来我觉得就是

由于不用自己做的配置，报错时很难定位。


### [7、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#7springboot-的核心注解是哪个它主要由哪几个注解组成的)  


启动类上面的注解是@SpringBootApplication，它也是 SpringBoot 的核心注解，主要组合包含了以下 3 个注解：

@SpringBootConfiguration：组合了 [@Configuration ](/Configuration ) 注解，实现配置文件的功能。

@EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能：

[@SpringBootApplication(exclude ](/SpringBootApplication(exclude ) = { DataSourceAutoConfiguration.class })。

@ComponentScan：Spring组件扫描。


### [8、什么是嵌入式服务器？我们为什么要使用嵌入式服务器呢?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#8什么是嵌入式服务器我们为什么要使用嵌入式服务器呢)  


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


### [9、SpringBoot 的自动配置是如何实现的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#9springboot-的自动配置是如何实现的)  


SpringBoot 项目的启动注解是：@SpringBootApplication，其实它就是由下面三个注解组成的：

**1、** [@Configuration ](/Configuration )

**2、** [@ComponentScan ](/ComponentScan )

**3、** @EnableAutoConfiguration

其中 @EnableAutoConfiguration 是实现自动配置的入口，该注解又通过 [@Import ](/Import ) 注解导入了AutoConfigurationImportSelector，在该类中加载 META-INF/spring.factories 的配置信息。然后筛选出以 EnableAutoConfiguration 为 key 的数据，加载到 IOC 容器中，实现自动配置功能！


### [10、什么是FreeMarker模板？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题，高级面试题及附答案解析.md#10什么是freemarker模板)  


FreeMarker是一个基于Java的模板引擎，最初专注于使用MVC软件架构进行动态网页生成。使用Freemarker的主要优点是表示层和业务层的完全分离。程序员可以处理应用程序代码，而设计人员可以处理html页面设计。最后使用freemarker可以将这些结合起来，给出最终的输出页面。


### 11、如何在 SpringBoot 启动的时候运行一些特定的代码？
### 12、SpringBoot 还提供了其它的哪些 Starter Project Options？
### 13、什么是 SpringBoot？
### 14、什么是执行器停机？
### 15、什么是JavaConfig？
### 16、SpringBoot 中如何实现定时任务 ?
### 17、Spring 、SpringBoot 和 Spring Cloud 的关系?
### 18、什么是 FreeMarker 模板？
### 19、RequestMapping 和 GetMapping 的不同之处在哪里？
### 20、如何使用 SpringBoot 实现全局异常处理？
### 21、我们如何监视所有SpringBoot微服务？
### 22、SpringBoot 自动配置原理是什么？
### 23、SpringBoot的核心注解是哪个？它主要由哪几个注解组成的？
### 24、SpringBoot的启动器有哪几种?
### 25、YAML 配置的优势在哪里 ?
### 26、如何重新加载 SpringBoot上的更改，而无需重新启动服务器？
### 27、SpringBoot 支持哪些日志框架？推荐和默认的日志框架是哪个？
### 28、SpringBoot 的配置文件有哪几种格式？它们有什么区别？
### 29、什么是SpringBoot ？
### 30、SpringBoot 实现热部署有哪几种方式？
### 31、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




