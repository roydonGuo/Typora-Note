# Spring最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、spring DAO 有什么用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#1spring-dao-有什么用)  


Spring DAO 使得 JDBC，Hibernate 或 JDO 这样的数据访问技术更容易以一种统一的方式工作。这使得用户容易在持久性技术之间切换。它还允许您在编写代码时，无需考虑捕获每种技术不同的异常。


### [2、什么是端到端微服务测试？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#2什么是端到端微服务测试)  


端到端测试验证了工作流中的每个流程都正常运行。这可确保系统作为一个整体协同工作并满足所有要求。

通俗地说，你可以说端到端测试是一种测试，在特定时期后测试所有东西。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_17.png#alt=img%5C_17.png)

图14：测试层次 – 微服务面试问题


### [3、解释WEB 模块。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#3解释web-模块。)  


Spring的WEB模块是构建在application context 模块基础之上，提供一个适合web应用的上下文。这个模块也包括支持多种面向web的任务，如透明地处理多个文件上传请求和程序级请求参数的绑定到你的业务对象。它也有对Jakarta Struts的支持。


### [4、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#4springboot-的核心注解是哪个它主要由哪几个注解组成的)  


启动类上面的注解是@SpringBootApplication，它也是 SpringBoot 的核心注解，主要组合包含了以下 3 个注解：

@SpringBootConfiguration：组合了 [@Configuration ](/Configuration ) 注解，实现配置文件的功能。

@EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能： [@SpringBootApplication(exclude ](/SpringBootApplication(exclude ) = { DataSourceAutoConfiguration.class })。

@ComponentScan：Spring组件扫描。


### [5、spring 提供了哪些配置方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#5spring-提供了哪些配置方式)  


bean 所需的依赖项和服务在 XML 格式的配置文件中指定。 这些配置文件通常包含许多 bean 定义和特定于应用程序的配置选项。 它们通常以 bean 标签开头。

**例如：**

```
<bean id="studentbean" class="org.edureka.firstSpring.StudentBean">
     <property name="name" value="Edureka"></property>
</bean>
```

**基于注解配置**

您可以通过在相关的类，方法或字段声明上使用注解，将 bean 配置为组件类本身，而不是使用 XML 来描述 bean 装配。 默认情况下，Spring 容器中未打开注解装配。 因此，您需要在使用它之前在 Spring 配置文件中启用它。 例如：

context:annotation-config/

Spring 的 Java 配置是通过使用[@Bean ](/Bean ) 和 [@Configuration ](/Configuration ) 来实现。

[@Bean ](/Bean ) 注解扮演与 元素相同的角色。 [@Configuration ](/Configuration ) 类允许通过简单地调用同一个类中的其他[@Bean ](/Bean ) 方法来定义 bean 间依赖关系。

**例如：**

```
public class StudentConfig {
    @Bean
    public StudentBean myStudent() {
        return new StudentBean();
    }
}
```


### [6、SpringBoot需要独立的容器运行？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#6springboot需要独立的容器运行)  


SpringBoot不需要独立的容器就可以运行，因为在SpringBoot工程发布的jar文件里已经包含了tomcat的jar文件。SpringBoot运行的时候会创建tomcat对象，实现web服务功能。也可以将SpringBoot发布成war文件，放到tomcat文件里面运行


### [7、微服务之间是如何独立通讯的](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#7微服务之间是如何独立通讯的)  


**1、** 远程过程调用（Remote Procedure Invocation）：也就是我们常说的服务的注册与发现，直接通过远程过程调用来访问别的service。

**优点：**

简单，常见,因为没有中间件代理，系统更简单

**缺点：**

**1、** 只支持请求/响应的模式，不支持别的，比如通知、请求/异步响应、发布/订阅、发布/异步响应

**2、** 降低了可用性，因为客户端和服务端在请求过程中必须都是可用的

**2、** 消息：使用异步消息来做服务间通信。服务间通过消息管道来交换消息，从而通信。

**优点:**

**1、** 把客户端和服务端解耦，更松耦合

**2、** 提高可用性，因为消息中间件缓存了消息，直到消费者可以消费

**3、** 支持很多通信机制比如通知、请求/异步响应、发布/订阅、发布/异步响应

**缺点:**

消息中间件有额外的复杂


### [8、什么是CSRF攻击？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#8什么是csrf攻击)  


CSRF代表跨站请求伪造。这是一种攻击，迫使最终用户在当前通过身份验证的Web应用程序上执行不需要的操作。CSRF攻击专门针对状态改变请求，而不是数据窃取，因为攻击者无法查看对伪造请求的响应。


### [9、使用 Spring 有哪些方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#9使用-spring-有哪些方式)  


**使用 Spring 有以下方式：**

**1、** 作为一个成熟的 Spring Web 应用程序。

**2、** 作为第三方 Web 框架，使用 Spring Frameworks 中间层。

**3、** 用于远程使用。

**4、** 作为企业级 Java Bean，它可以包装现有的 POJO（Plain Old Java Objects）。


### [10、运行 SpringBoot 有哪几种方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新面试题，2021年面试题及答案汇总.md#10运行-springboot-有哪几种方式)  


打包用命令或者放到容器中运行

用 Maven/ Gradle 插件运行

直接执行 main 方法运行


### 11、SpringBoot Starter 的工作原理是什么？
### 12、微服务的优点
### 13、什么是Eureka的自我保护模式，
### 14、如何使用 SpringBoot 生成一个 WAR 文件？
### 15、Spring框架中的单例bean是线程安全的吗?
### 16、你如何理解 SpringBoot 配置加载顺序？
### 17、Spring、SpringBoot、SpringMVC的区别？
### 18、缓存机制：
### 19、Eureka如何 保证AP
### 20、SpringBoot 2.X 有什么新特性？与 1.X 有什么区别？
### 21、单片，SOA和微服务架构有什么区别？
### 22、什么是执行器停机？
### 23、什么是客户证书？
### 24、什么是Hystrix?
### 25、SpringBoot 有哪几种读取配置的方式？
### 26、MVC是什么？MVC设计模式的好处有哪些
### 27、什么是SpringBoot？
### 28、XMLBeanFactory
### 29、服务降级底层是如何实现的？
### 30、Spring Cloud和SpringBoot版本对应关系
### 31、有哪些不同类型的IOC（依赖注入）方式？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




