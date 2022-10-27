# SpringBoot最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是WebSockets？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#1什么是websockets)  


WebSocket是一种计算机通信协议，通过单个TCP连接提供全双工通信信道。

![img_2.png][img_0826_04_2.png]

**1、** WebSocket是双向的 -使用WebSocket客户端或服务器可以发起消息发送。

**2、** WebSocket是全双工的 -客户端和服务器通信是相互独立的。

**3、** 单个TCP连接 -初始连接使用HTTP，然后将此连接升级到基于套接字的连接。然后这个单一连接用于所有未来的通信

**4、** Light -与http相比，WebSocket消息数据交换要轻得多。


### [2、什么是SpringBoot？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#2什么是springboot)  


多年来，随着新功能的增加，spring变得越来越复杂。只需访问https://spring.io/projects

如果必须启动一个新的Spring项目，我们必须添加构建路径或添加Maven依赖关系，配置应用程序服务器，添加spring配置。

因此，开始一个新的spring项目需要很多努力，因为我们现在必须从头开始做所有事情。

SpringBoot是解决这个问题的方法。SpringBoot已经建立在现有spring框架之上。使用spring启动，我们避免了之前我们必须做的所有样板代码和配置。

因此，SpringBoot可以帮助我们以最少的工作量，更加健壮地使用现有的Spring功能。


### [3、如何集成 SpringBoot 和 ActiveMQ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#3如何集成-springboot-和-activemq)  


对于集成 SpringBoot 和 ActiveMQ，我们使用依赖关系。它只需要很少的配置，并且不需要样板代码。


### [4、SpringBoot 2.X 有什么新特性？与 1.X 有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#4springboot-2x-有什么新特性与-1x-有什么区别)  


配置变更

JDK 版本升级

第三方类库升级

响应式 Spring 编程支持

HTTP/2 支持

配置属性绑定

更多改进与加强…


### [5、什么是YAML？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#5什么是yaml)  


YAML是一种人类可读的数据序列化语言。它通常用于配置文件。

与属性文件相比，如果我们想要在配置文件中添加复杂的属性，YAML文件就更加结构化，而且更少混淆。可以看出YAML具有分层配置数据。


### [6、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#6springboot-的核心注解是哪个它主要由哪几个注解组成的)  


启动类上面的注解是@SpringBootApplication，它也是 SpringBoot 的核心注解，主要组合包含了以下 3 个注解：

@SpringBootConfiguration：组合了 [@Configuration ](/Configuration ) 注解，实现配置文件的功能。

[@EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能：@SpringBootApplication(exclude ](/EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能：@SpringBootApplication(exclude ) = { DataSourceAutoConfiguration.class })。

@ComponentScan：Spring组件扫描。


### [7、保护 SpringBoot 应用有哪些方法？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#7保护-springboot-应用有哪些方法)  


**1、**  在生产中使用HTTPS

**2、**  使用Snyk检查你的依赖关系

**3、**  升级到最新版本

**4、**  启用CSRF保护

**5、**  使用内容安全策略防止XSS攻击


### [8、如何在不使用BasePACKAGE过滤器的情况下排除程序包？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#8如何在不使用basepackage过滤器的情况下排除程序包)  


过滤程序包的方法不尽相同。但是弹簧启动提供了一个更复杂的选项，可以在不接触组件扫描的情况下实现这一点。在使用注释@ SpringBootApplication时，可以使用排除属性。请参阅下面的代码片段：

@SpringBootApplication(exclude= {Employee.class})

public class FooAppConfiguration {}


### [9、微服务中如何实现 session 共享 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#9微服务中如何实现-session-共享-)  


在微服务中，一个完整的项目被拆分成多个不相同的独立的服务，各个服务独立部署在不同的服务器上，各自的 session 被从物理空间上隔离开了，但是经常，我们需要在不同微服务之间共享 session ，常见的方案就是 Spring Session + Redis 来实现 session 共享。将所有微服务的 session 统一保存在 Redis 上，当各个微服务对 session 有相关的读写操作时，都去操作 Redis 上的 session 。这样就实现了 session 共享，Spring Session 基于 Spring 中的代理过滤器实现，使得 session 的同步操作对开发人员而言是透明的，非常简便。


### [10、如何实现 SpringBoot应用程序的安全性?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题及答案附答案汇总.md#10如何实现-springboot应用程序的安全性)  


使用 `spring--startersecurityboot`--依赖项，并且必须添加安全配置。配置类将必须扩展 `WebSecurityConfigurerAdapter`并覆盖其方法。


### 11、是否可以在SpringBoot中覆盖或替换嵌入式Tomcat？
### 12、如何重新加载SpringBoot上的更改，而无需重新启动服务器？
### 13、项目中前后端分离部署，所以需要解决跨域的问题。
### 14、SpringBoot 有哪几种读取配置的方式？
### 15、SpringBoot读取配置文件的方式
### 16、SpringBoot 中如何解决跨域问题 ?
### 17、SpringBoot Starter的工作原理
### 18、如何使用SpringBoot实现分页和排序？
### 19、如何在 SpringBoot中禁用 Actuator端点安全性?
### 20、如何集成SpringBoot和ActiveMQ？
### 21、比较一下 Spring Security 和 Shiro 各自的优缺点 ?
### 22、什么是嵌入式服务器？我们为什么要使用嵌入式服务器呢?
### 23、SpringBoot 的核心配置文件有哪几个？它们的区别是什么？
### 24、如何重新加载SpringBoot上的更改，而无需重新启动服务器？
### 25、SpringBoot 需要独立的容器运行吗？
### 26、如何在自定义端口上运行 SpringBoot应用程序?
### 27、SpringBoot事物的使用
### 28、SpringBoot 提供了哪些核心功能？
### 29、微服务同时调用多个接口，怎么支持事务的啊？
### 30、如何实现 SpringBoot 应用程序的安全性？
### 31、SpringBoot 2.X 有什么新特性？与 1.X 有什么区别？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




