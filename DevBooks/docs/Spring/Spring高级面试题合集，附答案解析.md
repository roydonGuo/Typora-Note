# Spring高级面试题合集，附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、既然Nginx可以实现网关？为什么还需要使用Zuul框架](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#1既然nginx可以实现网关为什么还需要使用zuul框架)  


Zuul是SpringCloud集成的网关，使用Java语言编写，可以对SpringCloud架构提供更灵活的服务。


### [2、JPA 和 Hibernate 有哪些区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#2jpa-和-hibernate-有哪些区别)  


简而言之

JPA 是一个规范或者接口

Hibernate 是 JPA 的一个实现

当我们使用 JPA 的时候，我们使用 javax.persistence 包中的注释和接口时，不需要使用 hibernate 的导入包。

我们建议使用 JPA 注释，因为哦我们没有将其绑定到 Hibernate 作为实现。后来（我知道 - 小于百分之一的几率），我们可以使用另一种 JPA 实现。


### [3、什么是持续监测？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#3什么是持续监测)  


持续监控深入监控覆盖范围，从浏览器内前端性能指标，到应用程序性能，再到主机虚拟化基础架构指标。


### [4、Spring 应用程序有哪些不同组件？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#4spring-应用程序有哪些不同组件)  


**Spring 应用一般有以下组件：**

**1、** 接口 - 定义功能。

**2、** Bean 类 - 它包含属性，setter 和 getter 方法，函数等。

**3、** Spring 面向切面编程（AOP） - 提供面向切面编程的功能。

**4、** Bean 配置文件 - 包含类的信息以及如何配置它们。

**5、** 用户程序 - 它使用接口。


### [5、服务注册和发现是什么意思？Spring Cloud如何实现？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#5服务注册和发现是什么意思spring-cloud如何实现)  


当我们开始一个项目时，我们通常在属性文件中进行所有的配置。随着越来越多的服务开发和部署，添加和修改这些属性变得更加复杂。有些服务可能会下降，而某些位置可能会发生变化。手动更改属性可能会产生问题。Eureka服务注册和发现可以在这种情况下提供帮助。由于所有服务都在Eureka服务器上注册并通过调用Eureka服务器完成查找，因此无需处理服务地点的任何更改和处理。


### [6、项目中前后端分离部署，所以需要解决跨域的问题。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#6项目中前后端分离部署所以需要解决跨域的问题。)  


我们使用cookie存放用户登录的信息，在spring拦截器进行权限控制，当权限不符合时，直接返回给用户固定的json结果。

当用户登录以后，正常使用；当用户退出登录状态时或者token过期时，由于拦截器和跨域的顺序有问题，出现了跨域的现象。

我们知道一个http请求，先走filter，到达servlet后才进行拦截器的处理，如果我们把cors放在filter里，就可以优先于权限拦截器执行。

```
@Configuration
public class CorsConfig {

    @Bean
    public CorsFilter corsFilter() {
        CorsConfiguration corsConfiguration = new CorsConfiguration();
        corsConfiguration.addAllowedOrigin("*");
        corsConfiguration.addAllowedHeader("*");
        corsConfiguration.addAllowedMethod("*");
        corsConfiguration.setAllowCredentials(true);
        UrlBasedCorsConfigurationSource urlBasedCorsConfigurationSource = new UrlBasedCorsConfigurationSource();
        urlBasedCorsConfigurationSource.registerCorsConfiguration("/**", corsConfiguration);
        return new CorsFilter(urlBasedCorsConfigurationSource);
    }

}
```


### [7、Spring Cloud Stream](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#7spring-cloud-stream)  


轻量级事件驱动微服务框架，可以使用简单的声明式模型来发送及接收消息，主要实现为Apache Kafka及RabbitMQ。


### [8、如何设置服务发现？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#8如何设置服务发现)  


有多种方法可以设置服务发现。我将选择我认为效率最高的那个，Netflix的Eureka。这是一个简单的程序，不会对应用程序造成太大影响。此外，它支持多种类型的Web应用程序。 Eureka配置包括两个步骤 - 客户端配置和服务器配置。

使用属性文件可以轻松完成客户端配置。在clas spath中，Eureka搜索一个eureka-client.properties文件。它还搜索由特定于环境的属性文件中的环境引起的覆盖。

对于服务器配置，您必须首先配置客户端。完成后，服务器启动一个客户端，该客户端用于查找其他服务器。。默认情况下，Eureka服务器使用客户端配置来查找对等服务器。


### [9、path=”users”, collectionResourceRel=”users” 如何与 Spring Data Rest 一起使用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#9path=users,-collectionresourcerel=users-如何与-spring-data-rest-一起使用)  


path- 这个资源要导出的路径段。

collectionResourceRel- 生成指向集合资源的链接时使用的 rel 值。在生成 HATEOAS 链接时使用。


### [10、Spring Cloud 实现服务注册和发现的原理是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring高级面试题合集，附答案解析.md#10spring-cloud-实现服务注册和发现的原理是什么)  


**1、** 服务在发布时指定对应的服务名（服务名包括了 IP 地址和端口）将服务注册到注册中心（Eureka 或者 Zookeeper）这一过程是 Spring Cloud 自动实现的，只需要在 main 方法添加 @EnableDisscoveryClient 即可，同一个服务修改端口就可以启动多个实例。

**2、** 调用方法：传递服务名称通过注册中心获取所有的可用实例，通过负载均衡策略调用（Ribbon 和 Feign）对应的服务。


### 11、我们可以用微服务创建状态机吗？
### 12、开启 SpringBoot 特性有哪几种方式？
### 13、Spring MVC怎么样设定重定向和转发的？
### 14、开启 SpringBoot 特性有哪几种方式？
### 15、Zuul与Nginx有什么区别？
### 16、Spring MVC用什么对象从后台向前台传递数据的？
### 17、什么是编织（Weaving）？
### 18、各服务之间通信，对Restful和Rpc这2种方式如何做选择？
### 19、什么是YAML?
### 20、如何使用SpringBoot实现分页和排序？
### 21、如何在不使用BasePACKAGE过滤器的情况下排除程序包？
### 22、是否可以在Spring boot中更改嵌入式Tomcat服务器的端口?
### 23、什么是Feign？
### 24、SpringBoot 是否可以使用 XML 配置 ?
### 25、PACT如何运作？
### 26、解释AOP
### 27、Ribbon和Feign的区别？
### 28、如何实现 SpringBoot应用程序的安全性?
### 29、您对Distributed Transaction有何了解？
### 30、什么是WebSockets？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




