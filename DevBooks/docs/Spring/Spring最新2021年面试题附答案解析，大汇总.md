# Spring最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、SpringBoot 的配置文件有哪几种格式？它们有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#1springboot-的配置文件有哪几种格式它们有什么区别)  


.properties 和 .yml，它们的区别主要是书写格式不同。

**1、** properties

```
app.user.name = javastack
```

**2、** yml

```
app:
 user:
 name: javastack
```

另外，.yml 格式不支持 [@PropertySource ](/PropertySource ) 注解导入配置。


### [2、如何重新加载 SpringBoot上的更改，而无需重新启动服务器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#2如何重新加载-springboot上的更改而无需重新启动服务器)  


使用DEV工具来实现。 通过这种依赖关系，可以节省任何更改，嵌入式 tomcat将重新启动。 使用SpringBoot有一个开发工具`Dev Tools`模块，可以重新加载 SpringBoot上的更改，而无需重新启动服务器。消除每次手动部署更改的需要。 SpringBoot在发布它的第一个版本时没有这个功能。该模块将在生产环境中被禁用。它还提供H2数据库控制台以更好地测试应用程序。


### [3、创建一个 SpringBoot Project 的最简单的方法是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#3创建一个-springboot-project-的最简单的方法是什么)  


Spring Initializr是启动 SpringBoot Projects 的一个很好的工具。

**我们需要做一下几步：**

**1、** 登录 Spring Initializr，按照以下方式进行选择：

**2、** 选择 com.in28minutes.SpringBoot 为组

**3、** 选择 studet-services 为组件

**4、** 选择下面的依赖项

Web

Actuator

DevTools

**5、** 点击生 GenerateProject

**6、** 将项目导入 Eclipse。文件 - 导入 - 现有的 Maven 项目


### [4、SpringBoot 2、X 有什么新特性？与 1、X 有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#4springboot-2x-有什么新特性与-1x-有什么区别)  


**1、**  配置变更

**2、**  JDK 版本升级

**3、**  第三方类库升级

**4、**  响应式 Spring 编程支持

**5、**  HTTP/2 支持

**6、**  配置属性绑定

**7、**  更多改进与加强


### [5、为什么要选择微服务架构？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#5为什么要选择微服务架构)  


这是一个非常常见的微服务面试问题，你应该准备好了！微服务架构提供了许多优点。这里有几个：

**1、** 微服务可以轻松适应其他框架或技术。

**2、** 单个进程的失败不会影响整个系统。

**3、** 为大企业和小型团队提供支持。

**4、** 可以在相对较短的时间内独立部署。


### [6、什么是 CSRF 攻击？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#6什么是-csrf-攻击)  


CSRF 代表跨站请求伪造。这是一种攻击，迫使最终用户在当前通过身份验证的Web 应用程序上执行不需要的操作。CSRF 攻击专门针对状态改变请求，而不是数据窃取，因为攻击者无法查看对伪造请求的响应。


### [7、什么是SpringBoot？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#7什么是springboot)  


多年来，随着新功能的增加，spring变得越来越复杂。只需访问https://spring.io/projects 页面，我们就会看到可以在我们的应用程序中使用的所有Spring项目的不同功能。如果必须启动一个新的Spring项目，我们必须添加构建路径或添加Maven依赖关系，配置应用程序服务器，添加spring配置。因此，开始一个新的spring项目需要很多努力，因为我们现在必须从头开始做所有事情。

SpringBoot是解决这个问题的方法。SpringBoot已经建立在现有spring框架之上。使用spring启动，我们避免了之前我们必须做的所有样板代码和配置。因此，SpringBoot可以帮助我们以最少的工作量，更加健壮地使用现有的Spring功能。


### [8、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#8springboot-的核心注解是哪个它主要由哪几个注解组成的)  


启动类上面的注解是@SpringBootApplication，它也是 SpringBoot 的核心注解，主要组合包含了以下 3 个注解：

@SpringBootConfiguration：组合了 [@Configuration ](/Configuration ) 注解，实现配置文件的功能。

@EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能：

[@SpringBootApplication(exclude ](/SpringBootApplication(exclude ) = { DataSourceAutoConfiguration.class })。

@ComponentScan：Spring组件扫描。


### [9、为什么我们需要微服务容器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#9为什么我们需要微服务容器)  


要管理基于微服务的应用程序，容器是最简单的选择。它帮助用户单独部署和开发。您还可以使用Docker将微服务封装到容器的镜像中。没有任何额外的依赖或工作，微服务可以使用这些元素。


### [10、微服务之间是如何独⽴通讯的](https://gitee.com/souyunku/DevBooks/blob/master/docs/Spring/Spring最新2021年面试题附答案解析，大汇总.md#10微服务之间是如何独⽴通讯的)  


**1、** Dubbo 使⽤的是 RPC 通信，⼆进制传输，占⽤带宽⼩；

**2、** Spring Cloud 使⽤的是 HTTP RESTFul ⽅式。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/01/44/45_2.png#alt=45%5C_2.png)


### 11、SpringBoot 实现热部署有哪几种方式？
### 12、Spring MVC 框架有什么用？
### 13、微服务架构有哪些优势？
### 14、SpringBoot 有哪几种读取配置的方式？
### 15、列举 Spring Framework 的优点。
### 16、运行 SpringBoot 有哪几种方式？
### 17、Spring Cloud Bus
### 18、spring-boot-starter-parent 有什么用 ?
### 19、解释不同方式的自动装配
### 20、什么是耦合？
### 21、为什么人们会犹豫使用微服务？
### 22、运行 SpringBoot 有哪几种方式？
### 23、什么是无所不在的语言？
### 24、有哪些不同类型的IOC（依赖注入）方式？
### 25、SpringCloud Config 可以实现实时刷新吗？
### 26、如何在自定义端口上运行 SpringBoot 应用程序？
### 27、为什么我们需要 spring-boot-maven-plugin?
### 28、什么是JavaConfig？
### 29、列举 Spring Framework 的优点。
### 30、负载平衡的意义什么？
### 31、spring cloud 断路器的作用是什么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




