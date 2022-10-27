# Spring面试题大汇总，2022年附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、SpringBoot常用的starter有哪些?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#1springboot常用的starter有哪些)  


**1、** `spring-boot-starter-web` (嵌入tomcat和web开发需要servlet与jsp支持)

**2、** `spring-boot-starter-data-jpa` (数据库支持)

**3、** `spring-boot-starter-data-Redis` (Redis数据库支持)

**4、** `spring-boot-starter-data-solr` (solr搜索应用框架支持)

**5、** `mybatis-spring-boot-starter` (第三方的mybatis集成starter)


### [2、前后端分离，如何维护接口文档 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#2前后端分离如何维护接口文档-)  


前后端分离开发日益流行，大部分情况下，我们都是通过 SpringBoot 做前后端分离开发，前后端分离一定会有接口文档，不然会前后端会深深陷入到扯皮中。一个比较笨的方法就是使用 word 或者 md 来维护接口文档，但是效率太低，接口一变，所有人手上的文档都得变。在 SpringBoot 中，这个问题常见的解决方案是 Swagger ，使用 Swagger 我们可以快速生成一个接口文档网站，接口一旦发生变化，文档就会自动更新，所有开发工程师访问这一个在线网站就可以获取到最新的接口文档，非常方便。


### [3、有几种不同类型的自动代理？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#3有几种不同类型的自动代理)  


BeanNameAutoProxyCreator

DefaultAdvisorAutoProxyCreator

Metadata autoproxying


### [4、什么是FreeMarker模板？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#4什么是freemarker模板)  


FreeMarker是一个基于Java的模板引擎，最初专注于使用MVC软件架构进行动态网页生成。使用Freemarker的主要优点是表示层和业务层的完全分离。程序员可以处理应用程序代码，而设计人员可以处理html页面设计。最后使用freemarker可以将这些结合起来，给出最终的输出页面。


### [5、什么是持续集成（CI）？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#5什么是持续集成ci)  


持续集成（CI）是每次团队成员提交版本控制更改时自动构建和测试代码的过程。这鼓励开发人员通过在每个小任务完成后将更改合并到共享版本控制存储库来共享代码和单元测试。


### [6、Spring MVC的优点](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#6spring-mvc的优点)  


**1、** 可以支持各种视图技术,而不仅仅局限于JSP；

**2、** 与Spring框架集成（如IoC容器、AOP等）；

**3、** 清晰的角色分配：前端控制器(dispatcherServlet) , 请求到处理器映射（handlerMapping), 处理器适配器（HandlerAdapter), 视图解析器（ViewResolver）。

**4、** 支持各种请求资源的映射策略。


### [7、Spring Initializr 是创建 SpringBoot Projects 的唯一方法吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#7spring-initializr-是创建-springboot-projects-的唯一方法吗)  


不是的。

Spring Initiatlizr 让创建 SpringBoot 项目变的很容易，但是，你也可以通过设置一个 maven 项目并添加正确的依赖项来开始一个项目。

在我们的 Spring 课程中，我们使用两种方法来创建项目。

第一种方法是 start.spring.io 。

另外一种方法是在项目的标题为“Basic Web Application”处进行手动设置。

手动设置一个 maven 项目

**这里有几个重要的步骤：**

**1、** 在 Eclipse 中，使用文件 - 新建 Maven 项目来创建一个新项目

**2、** 添加依赖项。

**3、** 添加 maven 插件。

**4、** 添加 SpringBoot 应用程序类。

到这里，准备工作已经做好！


### [8、使用Spring通过什么方式访问Hibernate?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#8使用spring通过什么方式访问hibernate)  


**在Spring中有两种方式访问Hibernate：**

控制反转 Hibernate Template和 Callback。

继承 HibernateDAOSupport提供一个AOP 拦截器。


### [9、什么是bean的自动装配？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#9什么是bean的自动装配)  


Spring 容器能够自动装配相互合作的bean，这意味着容器不需要和配置，能通过Bean工厂自动处理bean之间的协作。


### [10、[@Qualifier ](/Qualifier ) 注解](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题大汇总，2021年附答案解析.md#10[@qualifier-]/qualifier--注解)  


当有多个相同类型的bean却只有一个需要自动装配时，将[@Qualifier ](/Qualifier ) 注解和[@Autowire ](/Autowire ) 注解结合使用以消除这种混淆，指定需要装配的确切的bean。


### 11、Spring Cloud Config
### 12、YAML 配置的优势在哪里 ?
### 13、服务注册和发现是什么意思？Spring Cloud 如何实现？
### 14、SpringBoot 支持哪些日志框架？推荐和默认的日志框架是哪个？
### 15、什么是基于Java的Spring注解配置? 给一些注解的例子.
### 16、什么是 SpringBoot？
### 17、什么是Eureka
### 18、自动装配有哪些局限性 ?
### 19、什么是Swagger？你用SpringBoot实现了它吗？
### 20、Spring IoC 的实现机制。
### 21、[@Autowired ](/Autowired ) 注解有什么用？
### 22、RequestMapping 和 GetMapping 的不同之处在哪里？
### 23、开启 SpringBoot 特性有哪几种方式？
### 24、Spring支持的事务管理类型
### 25、什么是Spring Initializer?
### 26、Spring AOP and AspectJ AOP 有什么区别？
### 27、什么是不同类型的双因素身份认证？
### 28、SpringBoot与SpringCloud 区别
### 29、我们如何在测试中消除非决定论？
### 30、什么是Oauth？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




