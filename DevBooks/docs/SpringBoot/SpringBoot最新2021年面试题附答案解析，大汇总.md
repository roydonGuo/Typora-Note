# SpringBoot最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、在 Spring Initializer 中，如何改变一个项目的包名字？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#1在-spring-initializer-中如何改变一个项目的包名字)  


好消息是你可以定制它。点击链接“转到完整版本”。你可以配置你想要修改的包名称！


### [2、SpringBoot 的配置文件有哪几种格式？它们有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#2springboot-的配置文件有哪几种格式它们有什么区别)  


.properties 和 .yml，它们的区别主要是书写格式不同。

**properties**

```
app.user.name = javastack
```

**yml**

```
app:
  user:
    name: javastack
```


### [3、什么是 Swagger？你用 SpringBoot 实现了它吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#3什么是-swagger你用-springboot-实现了它吗)  


Swagger 广泛用于可视化 API，使用 Swagger UI 为前端开发人员提供在线沙箱。Swagger 是用于生成 RESTful Web 服务的可视化表示的工具，规范和完整框架实现。它使文档能够以与服务器相同的速度更新。当通过 Swagger 正确定义时，消费者可以使用最少量的实现逻辑来理解远程服务并与其进行交互。因此，Swagger消除了调用服务时的猜测。


### [4、spring boot 核心配置文件是什么？bootstrap、properties 和 application、properties 有何区别 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#4spring-boot-核心配置文件是什么bootstrapproperties-和-applicationproperties-有何区别-)  


单纯做 SpringBoot 开发，可能不太容易遇到 bootstrap、properties 配置文件，但是在结合 Spring Cloud 时，这个配置就会经常遇到了，特别是在需要加载一些远程配置文件的时侯。

spring boot 核心的两个配置文件：

bootstrap (、 yml 或者 、 properties)：boostrap 由父 ApplicationContext 加载的，比 applicaton 优先加载，配置在应用程序上下文的引导阶段生效。一般来说我们在 Spring Cloud 配置就会使用这个文件。且 boostrap 里面的属性不能被覆盖；

application (、 yml 或者 、 properties)： 由ApplicatonContext 加载，用于 spring boot 项目的自动化配置。


### [5、什么是Spring Initializer?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#5什么是spring-initializer)  


这个问题并不难，但面试官总是以此测试候选人的专业知识。

Spring Initializer是一个网络应用程序，它可以生成一个SpringBoot项目，包含快速启动所需的一切。和往常一样，我们需要一个好的项目框架；它有助于你正确创建项目结构/框架。


### [6、SpringBoot Starter 的工作原理是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#6springboot-starter-的工作原理是什么)  


SpringBoot 在启动的时候会干这几件事情：

**1、** SpringBoot 在启动时会去依赖的 Starter 包中寻找 resources/META-INF/spring.factories 文件，然后根据文件中配置的 Jar 包去扫描项目所依赖的 Jar 包。

**2、** 根据 spring.factories 配置加载 AutoConfigure 类

**3、** 根据 [@Conditional ](/Conditional ) 注解的条件，进行自动配置并将 Bean 注入 Spring Context

总结一下，其实就是 SpringBoot 在启动的时候，按照约定去读取 SpringBoot Starter 的配置信息，再根据配置信息对资源进行初始化，并注入到 Spring 容器中。这样 SpringBoot 启动完毕后，就已经准备好了一切资源，使用过程中直接注入对应 Bean 资源即可。

这只是简单的三连环问答，不知道有多少同学能够完整的回答出来。

其实 SpringBoot 中有很多的技术点可以挖掘，今天给大家整理了十个高频 SpringBoot 面试题，希望可以在后期的面试中帮助到大家。


### [7、SpringBoot 中的 starter 到底是什么 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#7springboot-中的-starter-到底是什么-)  


首先，这个 Starter 并非什么新的技术点，基本上还是基于 Spring 已有功能来实现的。首先它提供了一个自动化配置类，一般命名为 `XXXAutoConfiguration` ，在这个配置类中通过条件注解来决定一个配置是否生效（条件注解就是 Spring 中原本就有的），然后它还会提供一系列的默认配置，也允许开发者根据实际情况自定义相关配置，然后通过类型安全的属性(spring、factories)注入将这些配置属性注入进来，新注入的属性会代替掉默认属性。正因为如此，很多第三方框架，我们只需要引入依赖就可以直接使用了。当然，开发者也可以自定义 Starter


### [8、SpringBoot 最大的优势是什么呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#8springboot-最大的优势是什么呢)  


SpringBoot 的最大的优势是“约定优于配置“。“约定优于配置“是一种软件设计范式，开发人员按照约定的方式来进行编程，可以减少软件开发人员需做决定的数量，获得简单的好处，而又不失灵活性。

SpringBoot 中 “约定优于配置“的具体产品体现在哪里。

SpringBoot Starter、SpringBoot Jpa 都是“约定优于配置“的一种体现。都是通过“约定优于配置“的设计思路来设计的，SpringBoot Starter 在启动的过程中会根据约定的信息对资源进行初始化；SpringBoot Jpa 通过约定的方式来自动生成 Sql ，避免大量无效代码编写。具体详细可以参考：SpringBoot 为什么这么火？


### [9、SpringBoot集成mybatis的过程](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#9springboot集成mybatis的过程)  


添加mybatis的starter maven依赖

```
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.3.2</version>
</dependency>
```

在mybatis的接口中 添加@Mapper注解

在application.yml配置数据源信息


### [10、如何集成SpringBoot和ActiveMQ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题附答案解析，大汇总.md#10如何集成springboot和activemq)  


对于集成SpringBoot和ActiveMQ，我们使用spring-boot-starter-activemq 依赖关系。 它只需要很少的配置，并且不需要样板代码。


### 11、如何在SpringBoot中禁用Actuator端点安全性？
### 12、RequestMapping 和 GetMapping 的不同之处在哪里？
### 13、SpringBoot的自动配置原理是什么
### 14、什么是 Spring Profiles？
### 15、spring-boot-starter-parent有什么用？
### 16、SpringBoot的配置文件有哪几种格式？区别是什么？
### 17、如何在 SpringBoot 中禁用 Actuator 端点安全性？
### 18、运行 SpringBoot 有哪几种方式？
### 19、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？
### 20、SpringBoot 怎么用好自动配置，精髓:
### 21、SpringBoot需要独立的容器运行？
### 22、如何重新加载 SpringBoot 上的更改，而无需重新启动服务器？SpringBoot项目如何热部署？
### 23、什么是Spring Batch？
### 24、@RestController和@Controller的区别
### 25、SpringBoot自动配置的原理
### 26、什么是JavaConfig？
### 27、比较一下 Spring Security 和 Shiro 各自的优缺点 ?
### 28、JPA 和 Hibernate 有哪些区别？JPA 可以支持动态 SQL 吗？
### 29、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？
### 30、path=”users”, collectionResourceRel=”users” 如何与 Spring Data Rest 一起使用？
### 31、SpringBoot有哪些优点？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




