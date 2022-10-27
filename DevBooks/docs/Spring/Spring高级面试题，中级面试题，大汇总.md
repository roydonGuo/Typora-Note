# Spring高级面试题，中级面试题，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Spring MVC的主要组件？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#1spring-mvc的主要组件)  


**1、** 前端控制器 DispatcherServlet（不需要程序员开发）

**作用：**

接收请求、响应结果，相当于转发器，有了DispatcherServlet 就减少了其它组件之间的耦合度。

**2、** 处理器映射器HandlerMapping（不需要程序员开发）

**作用：**

根据请求的URL来查找Handler

**3、** 处理器适配器HandlerAdapter

**注意：**

在编写Handler的时候要按照HandlerAdapter要求的规则去编写，这样适配器HandlerAdapter才可以正确的去执行Handler。

**4、** 处理器Handler（需要程序员开发）

**5、** 视图解析器 ViewResolver（不需要程序员开发）

**作用：**

进行视图的解析，根据视图逻辑名解析成真正的视图（view）

**6、** 视图View（需要程序员开发jsp）

View是一个接口， 它的实现类支持不同的视图类型（jsp，freemarker，pdf等等）


### [2、什么是Hystrix？它如何实现容错？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#2什么是hystrix它如何实现容错)  


Hystrix是一个延迟和容错库，旨在隔离远程系统，服务和第三方库的访问点，当出现故障是不可避免的故障时，停止级联故障并在复杂的分布式系统中实现弹性。

通常对于使用微服务架构开发的系统，涉及到许多微服务。这些微服务彼此协作。

思考以下微服务

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0814/02/img_2.png#alt=img%5C_2.png)

假设如果上图中的微服务9失败了，那么使用传统方法我们将传播一个异常。但这仍然会导致整个系统崩溃。

随着微服务数量的增加，这个问题变得更加复杂。微服务的数量可以高达1000.这是hystrix出现的地方 我们将使用Hystrix在这种情况下的Fallback方法功能。我们有两个服务employee-consumer使用由employee-consumer公开的服务。

简化图如下所示

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0814/02/img_3.png#alt=img%5C_3.png)

现在假设由于某种原因，employee-producer公开的服务会抛出异常。我们在这种情况下使用Hystrix定义了一个回退方法。这种后备方法应该具有与公开服务相同的返回类型。如果暴露服务中出现异常，则回退方法将返回一些值。


### [3、什么是 JavaConfig？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#3什么是-javaconfig)  


Spring JavaConfig 是 Spring 社区的产品，Spring 3、0引入了他，它提供了配置 Spring IOC 容器的纯Java 方法。因此它有助于避免使用 XML 配置。使用 JavaConfig 的优点在于：

面向对象的配置。由于配置被定义为 JavaConfig 中的类，因此用户可以充分利用 Java 中的面向对象功能。一个配置类可以继承另一个，重写它的[@Bean ](/Bean ) 方法等。

减少或消除 XML 配置。基于依赖注入原则的外化配置的好处已被证明。但是，许多开发人员不希望在 XML 和 Java 之间来回切换。JavaConfig 为开发人员提供了一种纯 Java 方法来配置与 XML 配置概念相似的 Spring 容器。从技术角度来讲，只使用 JavaConfig 配置类来配置容器是可行的，但实际上很多人认为将JavaConfig 与 XML 混合匹配是理想的。

类型安全和重构友好。JavaConfig 提供了一种类型安全的方法来配置 Spring容器。由于 Java 5、0 对泛型的支持，现在可以按类型而不是按名称检索 bean，不需要任何强制转换或基于字符串的查找。

**常用的Java config：**

@Configuration：在类上打上写下此注解，表示这个类是配置类

@ComponentScan：在配置类上添加 [@ComponentScan ](/ComponentScan ) 注解。该注解默认会扫描该类所在的包下所有的配置类，相当于之前的 <context:component-scan >。

@Bean：bean的注入：相当于以前的< bean id="objectMapper" class="org、codehaus、jackson、map、ObjectMapper" />

@EnableWebMvc：相当于xml的<mvc:annotation-driven >

@ImportResource： 相当于xml的 < import resource="applicationContext-cache、xml">


### [4、SpringBoot 中如何实现定时任务 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#4springboot-中如何实现定时任务-)  


定时任务也是一个常见的需求，SpringBoot 中对于定时任务的支持主要还是来自 Spring 框架。

在 SpringBoot 中使用定时任务主要有两种不同的方式，一个就是使用 Spring 中的 [@Scheduled ](/Scheduled ) 注解，另一个则是使用第三方框架 Quartz。

使用 Spring 中的 [@Scheduled ](/Scheduled ) 的方式主要通过 [@Scheduled ](/Scheduled ) 注解来实现。

使用 Quartz ，则按照 Quartz 的方式，定义 Job 和 Trigger 即可。



### [5、SpringBoot 配置加载顺序?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#5springboot-配置加载顺序)  


**1、** properties文件 2、YAML文件 3、系统环境变量 4、命令行参数


### [6、康威定律是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#6康威定律是什么)  


康威定律指出，“设计系统的组织，其产生的设计等同于组织之内、组织之间的沟通结构。” 面试官可能会问反微服务面试问题，比如康威定律与微服务的关系。一些松散耦合的api形成了微服务的体系结构。这种结构非常适合小团队实现自治组件的方式。这种体系结构使组织在重组其工作流程时更加灵活。


### [7、SpringBoot有哪些优点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#7springboot有哪些优点)  


减少开发，测试时间和努力。

使用JavaConfig有助于避免使用XML。

避免大量的Maven导入和各种版本冲突。

提供意见发展方法。

通过提供默认值快速开始开发。

没有单独的Web服务器需要。这意味着你不再需要启动Tomcat，Glassfish或其他任何东西。

需要更少的配置 因为没有web.xml文件。只需添加用@ Configuration注释的类，然后添加用@Bean注释的方法，Spring将自动加载对象并像以前一样对其进行管理。您甚至可以将@Autowired添加到bean方法中，以使Spring自动装入需要的依赖关系中。基于环境的配置 使用这些属性，您可以将您正在使用的环境传递到应用程序：-Dspring.profiles.active = {enviornment}。在加载主应用程序属性文件后，Spring将在（application{environment} .properties）中加载后续的应用程序属性文件。


### [8、什么是 FreeMarker 模板？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#8什么是-freemarker-模板)  


FreeMarker 是一个基于 Java 的模板引擎，最初专注于使用 MVC 软件架构进行动态网页生成。使用 Freemarker 的主要优点是表示层和业务层的完全分离。程序员可以处理应用程序代码，而设计人员可以处理 html 页面设计。最后使用freemarker 可以将这些结合起来，给出最终的输出页面。


### [9、Spring Cloud Config](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#9spring-cloud-config)  


Config能够管理所有微服务的配置文件

集中配置管理工具，分布式系统中统一的外部配置管理，默认使用Git来存储配置，可以支持客户端配置的刷新及加密、解密操作。


### [10、什么是 SpringBoot？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题，中级面试题，大汇总.md#10什么是-springboot)  


SpringBoot 是 Spring 开源组织下的子项目，是 Spring 组件一站式解决方案，主要是简化了使用 Spring 的难度，简省了繁重的配置，提供了各种启动器，开发者能快速上手。


### 11、Spring Cloud OpenFeign
### 12、SpringBoot 支持哪些日志框架？推荐和默认的日志框架是哪个？
### 13、如何使用 SpringBoot 实现全局异常处理？
### 14、什么是JavaConfig？
### 15、为什么在微服务中需要Reports报告和Dashboards仪表板？
### 16、微服务的端到端测试意味着什么？
### 17、什么是Spring的依赖注入？
### 18、哪些是重要的bean生命周期方法？ 你能重载它们吗？
### 19、什么是 SpringBoot 启动类注解：
### 20、WebApplicationContext
### 21、SpringBoot 支持哪些日志框架？推荐和默认的日志框架是哪个？
### 22、使用 SpringBoot 开发分布式微服务时，我们面临什么问题
### 23、什么是基于注解的容器配置?
### 24、什么是SpringBoot
### 25、可以通过多少种方式完成依赖注入？
### 26、怎样在方法里面得到Request,或者Session？
### 27、eureka和zookeeper都可以提供服务注册与发现的功能，请说说两个的区别？
### 28、设计微服务的最佳实践是什么？
### 29、您对Mike Cohn的测试金字塔了解多少？
### 30、服务雪崩？
### 31、SpingMvc中的控制器的注解一般用哪个,有没有别的注解可以替代？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




