# Spring高级面试题及答案，2022版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、[@Qualifier ](/Qualifier ) 注解有什么用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#1[@qualifier-]/qualifier--注解有什么用)  


当您创建多个相同类型的 bean 并希望仅使用属性装配其中一个 bean 时，您可以使用[@Qualifier ](/Qualifier ) 注解和 [@Autowired ](/Autowired ) 通过指定应该装配哪个确切的 bean 来消除歧义。

例如，这里我们分别有两个类，Employee 和 EmpAccount。在 EmpAccount 中，使用[@Qualifier ](/Qualifier ) 指定了必须装配 id 为 emp1 的 bean。

Employee.java

```
public class Employee {
    private String name;
    @Autowired
    public void setName(String name) {
        this.name=name;
    }
    public string getName() {
        return name;
    }
}
```

EmpAccount.java

```
public class EmpAccount {
    private Employee emp;

    @Autowired
    @Qualifier(emp1)
    public void showName() {
        System.out.println(“Employee name : ”+emp.getName);
    }
}
```


### [2、DispatcherServlet](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#2dispatcherservlet)  


Spring的MVC框架是围绕DispatcherServlet来设计的，它用来处理所有的HTTP请求和响应。


### [3、SpringCloud有几种调用接口方式](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#3springcloud有几种调用接口方式)  


**1、** Feign

**2、** RestTemplate


### [4、什么是 Spring Data？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#4什么是-spring-data)  


来自：[//projects.spring.io/spring-](//projects.spring.io/spring-) data/

Spring Data 的使命是在保证底层数据存储特殊性的前提下，为数据访问提供一个熟悉的，一致性的，基于 Spring 的编程模型。这使得使用数据访问技术，关系数据库和非关系数据库，map-reduce 框架以及基于云的数据服务变得很容易。

为了让它更简单一些，Spring Data 提供了不受底层数据源限制的 Abstractions 接口。

你可以定义一简单的库，用来插入，更新，删除和检索代办事项，而不需要编写大量的代码。


### [5、创建一个 SpringBoot Project 的最简单的方法是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#5创建一个-springboot-project-的最简单的方法是什么)  


Spring Initializer 是创建 SpringBoot Projects 的一个很好的工具


### [6、解释Spring支持的几种bean的作用域。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#6解释spring支持的几种bean的作用域。)  


**Spring框架支持以下五种bean的作用域：**

**1、** singleton : bean在每个Spring ioc 容器中只有一个实例。

**2、** prototype：一个bean的定义可以有多个实例。

**3、** request：每次http请求都会创建一个bean，该作用域仅在基于web的Spring ApplicationContext情形下有效。

**4、** session：在一个HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。

**5、** global-session：在一个全局的HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。

缺省的Spring bean 的作用域是Singleton.


### [7、列举 Spring DAO 抛出的异常。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#7列举-spring-dao-抛出的异常。)  


![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/02/img_4.png#alt=img%5C_4.png)


### [8、什么是微服务中的反应性扩展？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#8什么是微服务中的反应性扩展)  


Reactive Extensions也称为Rx。这是一种设计方法，我们通过调用多个服务来收集结果，然后编译组合响应。这些调用可以是同步或异步，阻塞或非阻塞。Rx是分布式系统中非常流行的工具，与传统流程相反。

希望这些微服务面试问题可以帮助您进行微服务架构师访谈。

翻译来源：[https://www.edureka.co/blog/interview-questions/microservices-interview-questions/](https://www.edureka.co/blog/interview-questions/microservices-interview-questions/)



### [9、比较一下 Spring Security 和 Shiro 各自的优缺点 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#9比较一下-spring-security-和-shiro-各自的优缺点-)  


由于 SpringBoot 官方提供了大量的非常方便的开箱即用的 Starter ，包括 Spring Security 的 Starter ，使得在 SpringBoot 中使用 Spring Security 变得更加容易，甚至只需要添加一个依赖就可以保护所有的接口，所以，如果是 SpringBoot 项目，一般选择 Spring Security 。当然这只是一个建议的组合，单纯从技术上来说，无论怎么组合，都是没有问题的。Shiro 和 Spring Security 相比，主要有如下一些特点：

Spring Security 是一个重量级的安全管理框架；Shiro 则是一个轻量级的安全管理框架

Spring Security 概念复杂，配置繁琐；Shiro 概念简单、配置简单

Spring Security 功能强大；Shiro 功能简单


### [10、使用 Spring 访问 Hibernate 的方法有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题及答案，2021版.md#10使用-spring-访问-hibernate-的方法有哪些)  


我们可以通过两种方式使用 Spring 访问 Hibernate：

**1、** 使用 Hibernate 模板和回调进行控制反转

**2、** 扩展 HibernateDAOSupport 并应用 AOP 拦截器节点


### 11、bootstrap.yml和application.yml有什么区别?
### 12、SpringBoot有哪些优点？
### 13、为什么需要学习Spring Cloud
### 14、SpringBoot和springcloud认识
### 15、spring boot 核心配置文件是什么？bootstrap.properties 和 application.properties 有何区别 ?
### 16、列举微服务技术栈
### 17、21、在Spring MVC应用程序中使用WebMvcTest注释有什么用处？
### 18、您对微服务架构中的语义监控有何了解？
### 19、SpringBoot 中如何实现定时任务 ?
### 20、在微服务中，如何保护服务?
### 21、[@Controller ](/Controller ) 注解
### 22、SpringBoot Starter的工作原理
### 23、如何集成 SpringBoot 和 ActiveMQ？
### 24、如何重新加载 SpringBoot 上的更改，而无需重新启动服务器？SpringBoot项目如何热部署？
### 25、什么是 AOP切点
### 26、如何集成SpringBoot和ActiveMQ？
### 27、什么是消费者驱动的合同（CDC）？
### 28、在Spring框架中如何更有效地使用JDBC?
### 29、什么是领域驱动设计？
### 30、SpringBoot 2.X 有什么新特性？与 1.X 有什么区别？
### 31、SpringCloud 和 Dubbo 有哪些区别?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




