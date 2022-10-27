# Spring面试题及答案整理，2022年最新，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、您对微服务有何了解？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#1您对微服务有何了解)  


微服务，又称微服务架构，是一种架构风格，它将应用程序构建为以业务领域为模型的小型自治服务集合 。

通俗地说，你必须看到蜜蜂如何通过对齐六角形蜡细胞来构建它们的蜂窝状物。他们最初从使用各种材料的小部分开始，并继续从中构建一个大型蜂箱。这些细胞形成图案，产生坚固的结构，将蜂窝的特定部分固定在一起。这里，每个细胞独立于另一个细胞，但它也与其他细胞相关。这意味着对一个细胞的损害不会损害其他细胞，因此，蜜蜂可以在不影响完整蜂箱的情况下重建这些细胞。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_1.png#alt=img%5C_1.png)

图1：微服务的蜂窝表示 – 微服务访谈问题

请参考上图。这里，每个六边形形状代表单独的服务组件。与蜜蜂的工作类似，每个敏捷团队都使用可用的框架和所选的技术堆栈构建单独的服务组件。就像在蜂箱中一样，每个服务组件形成一个强大的微服务架构，以提供更好的可扩展性。此外，敏捷团队可以单独处理每个服务组件的问题，而对整个应用程序没有影响或影响最小。


### [2、SpringBoot微服务中如何实现 session 共享 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#2springboot微服务中如何实现-session-共享-)  


在微服务中，一个完整的项目被拆分成多个不相同的独立的服务，各个服务独立部署在不同的服务器上，各自的 session 被从物理空间上隔离开了，但是经常，我们需要在不同微服务之间共享 session ，常见的方案就是 Spring Session + Redis 来实现 session 共享。将所有微服务的 session 统一保存在 Redis 上，当各个微服务对 session 有相关的读写操作时，都去操作 Redis 上的 session 。这样就实现了 session 共享，Spring Session 基于 Spring 中的代理过滤器实现，使得 session 的同步操作对开发人员而言是透明的，非常简便。


### [3、SpringBoot的自动配置原理是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#3springboot的自动配置原理是什么)  


主要是SpringBoot的启动类上的核心注解SpringBootApplication注解主配置类，有了这个主配置类启动时就会为SpringBoot开启一个@EnableAutoConfiguration注解自动配置功能。

有了这个EnableAutoConfiguration的话就会：

**1、**  从配置文件META_INF/Spring、factories加载可能用到的自动配置类

**2、**  去重，并将exclude和excludeName属性携带的类排除

**3、**  过滤，将满足条件（@Conditional）的自动配置类返回


### [4、在 Spring中如何注入一个java集合？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#4在-spring中如何注入一个java集合)  


Spring提供以下几种集合的配置元素：

**1、** 类型用于注入一列值，允许有相同的值。

**2、**  类型用于注入一组值，不允许有相同的值。

**3、**  类型用于注入一组键值对，键和值都可以为任意类型。

**4、** 类型用于注入一组键值对，键和值都只能为String类型。


### [5、SpringBoot、Spring MVC 和 Spring 有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#5springbootspring-mvc-和-spring-有什么区别)  


**1、** Spring

Spring最重要的特征是依赖注入。所有 SpringModules 不是依赖注入就是 IOC 控制反转。

当我们恰当的使用 DI 或者是 IOC 的时候，我们可以开发松耦合应用。松耦合应用的单元测试可以很容易的进行。

**2、** Spring MVC

Spring MVC 提供了一种分离式的方法来开发 Web 应用。通过运用像 DispatcherServelet，MoudlAndView 和 ViewResolver 等一些简单的概念，开发 Web 应用将会变的非常简单。

**3、** SpringBoot

Spring 和 SpringMVC 的问题在于需要配置大量的参数。

SpringBoot 通过一个自动配置和启动的项来目解决这个问题。为了更快的构建产品就绪应用程序，SpringBoot 提供了一些非功能性特征。


### [6、Spring MVC怎么和AJAX相互调用的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#6spring-mvc怎么和ajax相互调用的)  


通过Jackson框架就可以把Java里面的对象直接转化成Js可以识别的Json对象。具体步骤如下 ：

**1、** 加入Jackson.jar

**2、** 在配置文件中配置json的映射

**3、** 在接受Ajax方法里面可以直接返回Object,List等,但方法前面要加上@ResponseBody注解。


### [7、解释AOP模块](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#7解释aop模块)  


AOP模块用于发给我们的Spring应用做面向切面的开发， 很多支持由AOP联盟提供，这样就确保了Spring和其他AOP框架的共通性。这个模块将元数据编程引入Spring。


### [8、如何在自定义端口上运行SpringBoot应用程序？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#8如何在自定义端口上运行springboot应用程序)  


为了在自定义端口上运行SpringBoot应用程序，您可以在application.properties中指定端口。

```
 server.port = 8090
```


### [9、什么是bean装配?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#9什么是bean装配)  


装配，或bean 装配是指在Spring 容器中把bean组装到一起，前提是容器需要知道bean的依赖关系，如何通过依赖注入来把它们装配到一起。


### [10、SpringBoot支持哪些嵌入式容器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring面试题及答案整理，2021年最新，汇总版.md#10springboot支持哪些嵌入式容器)  


无论何时创建Java应用程序，都可以通过两种方法进行部署： 使用外部的应用程序容器。 将容器嵌入jar文件中。 SpringBoot包含Jetty，Tomcat和Undertow服务器，所有服务器都是嵌入式的。 Jetty - 用于大量项目，Eclipse Jetty可以嵌入到框架，应用程序服务器，工具和集群中。 Tomcat - Apache Tomcat是一个开源JavaServer Pages实现，可以很好地与嵌入式系统配合使用。 Undertow - 一个灵活而突出的Web服务器，它使用小型单一处理程序来开发Web服务器。


### 11、分布式配置中心的作用？
### 12、SpringBoot读取配置文件的方式
### 13、@Component, @Controller, @Repository, [@Service ](/Service ) 有何区别？
### 14、哪种依赖注入方式你建议使用，构造器注入，还是 Setter方法注入？
### 15、如何实现SpringBoot应用程序的安全性？
### 16、请描述Spring MVC的工作流程？描述一下 DispatcherServlet 的工作流程？
### 17、Spring MVC与Struts2区别
### 18、SpringBoot的核心注解是哪个？它主要由哪几个注解组成的？
### 19、什么是 Aspect？
### 20、什么是 Spring Data ?
### 21、哪些是重要的bean生命周期方法？你能重载它们吗？
### 22、微服务设计的基础是什么？
### 23、SpringBoot 还提供了其它的哪些 Starter Project Options？
### 24、SpringBoot 实现热部署有哪几种方式？
### 25、SpringBoot有哪些优点？
### 26、一个 Spring Bean 定义 包含什么？
### 27、SpringBoot 自动配置原理是什么？
### 28、Spring Cloud 和dubbo区别?
### 29、你怎样定义类的作用域?
### 30、熔断的原理，以及如何恢复？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




