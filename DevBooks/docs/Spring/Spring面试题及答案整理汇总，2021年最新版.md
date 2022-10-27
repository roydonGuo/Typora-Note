# Spring面试题及答案整理汇总，2022年最新版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、区分 BeanFactory 和 ApplicationContext。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#1区分-beanfactory-和-applicationcontext。)  

| BeanFactory | ApplicationContext |
| --- | --- |
| 它使用懒加载 | 它使用即时加载 |
| 它使用语法显式提供资源对象 | 它自己创建和管理资源对象 |
| 不支持国际化 | 支持国际化 |
| 不支持基于依赖的注解 | 支持基于依赖的注解 |



### [2、如何重新加载SpringBoot上的更改，而无需重新启动服务器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#2如何重新加载springboot上的更改而无需重新启动服务器)  


这可以使用DEV工具来实现。通过这种依赖关系，您可以节省任何更改，嵌入式tomcat将重新启动。

SpringBoot有一个开发工具（DevTools）模块，它有助于提高开发人员的生产力。Java开发人员面临的一个主要挑战是将文件更改自动部署到服务器并自动重启服务器。

开发人员可以重新加载SpringBoot上的更改，而无需重新启动服务器。这将消除每次手动部署更改的需要。SpringBoot在它的第一个版本时没有这个功能。

这是开发人员最需要的功能。DevTools模块完全满足开发人员的需求。该模块将在生产环境中被禁用。它还提供H2数据库控制台以更好地测试应用程序。


### [3、spring JDBC API 中存在哪些类？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#3spring-jdbc-api-中存在哪些类)  


**1、** JdbcTemplate

**2、** SimpleJdbcTemplate

**3、** NamedParameterJdbcTemplate

**4、** SimpleJdbcInsert

**5、** SimpleJdbcCall


### [4、spring cloud 和dubbo区别?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#4spring-cloud-和dubbo区别)  


**1、** 服务调用方式 dubbo是RPC springcloud Rest Api

**2、** 注册中心,dubbo 是zookeeper springcloud是eureka，也可以是zookeeper

**3、** 服务网关,dubbo本身没有实现，只能通过其他第三方技术整合，springcloud有Zuul路由网关，作为路由服务器，进行消费者的请求分发,springcloud支持断路器，与git完美集成配置文件支持版本控制，事物总线实现配置文件的更新与服务自动装配等等一系列的微服务架构要素。


### [5、spring boot初始化环境变量流程?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#5spring-boot初始化环境变量流程)  


**1、** 调用`prepareEnvironment`方法去设置环境变量

**2、** 接下来有三个方法`getOrCreateEnvironment`，`configureEnvironment`，`environmentPrepared`

**3、** `getOrCreateEnvironment`去初始化系统环境变量

**4、** `configureEnvironment`去初始化命令行参数

**5、** `environmentPrepared`当广播到来的时候调用`onApplicationEnvironmentPreparedEvent`方法去使用`postProcessEnvironment`方法`load yml`和`properties变量`


### [6、服务网关的作用](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#6服务网关的作用)  


**1、** 简化客户端调用复杂度，统一处理外部请求。

**2、** 数据裁剪以及聚合，根据不同的接口需求，对数据加工后对外。

**3、** 多渠道支持，针对不同的客户端提供不同的网关支持。

**4、** 遗留系统的微服务化改造，可以作为新老系统的中转组件。

**5、** 统一处理调用过程中的安全、权限问题。


### [7、SpringBoot 支持哪些日志框架？推荐和默认的日志框架是哪个？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#7springboot-支持哪些日志框架推荐和默认的日志框架是哪个)  


SpringBoot 支持 Java Util Logging, Log4j2, Lockback 作为日志框架，如果你使用 Starters 启动器，SpringBoot 将使用 Logback 作为默认日志框架。


### [8、如何配置SpringBoot应用程序日志记录？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#8如何配置springboot应用程序日志记录)  


SpringBoot附带了对Log4J2，Java Util Logging和Logback的支持。它通常预先配置为控制台输出。可以通过仅在application.properties文件中指定logging.level来配置它们。

```
logging.level.spring.framework=Debug
```


### [9、Ribbon和Feign调用服务的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#9ribbon和feign调用服务的区别)  


**1、** 调用方式同：Ribbon需要我们自己构建Http请求，模拟Http请求然后通过RestTemplate发给其他服务，步骤相当繁琐

**2、** 而Feign则是在Ribbon的基础上进行了一次改进，采用接口的形式，将我们需要调用的服务方法定义成抽象方法保存在本地就可以了，不需要自己构建Http请求了，直接调用接口就行了，不过要注意，调用方法要和本地抽象方法的签名完全一致。


### [10、什么是 Swagger？你用 SpringBoot 实现了它吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理汇总，2021年最新版.md#10什么是-swagger你用-springboot-实现了它吗)  


Swagger 广泛用于可视化 API，使用 Swagger UI 为前端开发人员提供在线沙箱。Swagger 是用于生成 RESTful Web 服务的可视化表示的工具，规范和完整框架实现。它使文档能够以与服务器相同的速度更新。当通过 Swagger 正确定义时，消费者可以使用最少量的实现逻辑来理解远程服务并与其进行交互。因此，Swagger消除了调用服务时的猜测。


### 11、多个消费者调⽤同⼀接⼝，eruka默认的分配⽅式是什么？
### 12、什么是starter?
### 13、如何使用SpringBoot实现异常处理?
### 14、Bean 工厂和 Application contexts 有什么区别？
### 15、spring-boot-starter-parent有什么用？
### 16、微服务之间如何独立通讯的?
### 17、SpringBoot 有哪几种读取配置的方式？
### 18、你所知道微服务的技术栈有哪些？列举一二
### 19、Docker的目的是什么？
### 20、如何给Spring 容器提供配置元数据?
### 21、如何在SpringBoot应用程序中实现Spring安全性？
### 22、SpringBoot性能如何优化
### 23、什么是网关?
### 24、如何使用 SpringBoot 实现异常处理？
### 25、SpringBoot 中如何解决跨域问题 ?
### 26、指出在 spring aop 中 concern 和 cross-cutting concern 的不同之处。
### 27、谈谈服务降级、熔断、服务隔离
### 28、什么是 Spring Profiles？
### 29、什么是 WebSockets？
### 30、@Component, @Controller, @Repository, [@Service ](/Service ) 有何区别？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




