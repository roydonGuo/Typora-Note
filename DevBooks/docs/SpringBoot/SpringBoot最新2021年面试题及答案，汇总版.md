# SpringBoot最新2022年面试题及答案，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、spring-boot-starter-parent 有什么用 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#1spring-boot-starter-parent-有什么用-)  


我们都知道，新创建一个 SpringBoot 项目，默认都是有 parent 的，这个 parent 就是 spring-boot-starter-parent ，spring-boot-starter-parent 主要有如下作用：

**1、** 定义了 Java 编译版本为 1.8 。

**2、** 使用 UTF-8 格式编码。

**3、** 继承自 spring-boot-dependencies，这个里边定义了依赖的版本，也正是因为继承了这个依赖，所以我们在写依赖时才不需要写版本号。

**4、** 执行打包操作的配置。

**5、** 自动化的资源过滤。

**6、** 自动化的插件配置。

**7、** 针对 application.properties 和 application.yml 的资源过滤，包括通过 profile 定义的不同环境的配置文件，例如 application-dev.properties 和 application-dev.yml。


### [2、shiro和oauth还有cas他们之间的关系是什么？问下您公司权限是如何设计，还有就是这几个概念的区别。](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#2shiro和oauth还有cas他们之间的关系是什么问下您公司权限是如何设计还有就是这几个概念的区别。)  


cas和oauth是一个解决单点登录的组件，shiro主要是负责权限安全方面的工作，所以功能点不一致。但往往需要单点登陆和权限控制一起来使用，所以就有 cas+shiro或者oauth+shiro这样的组合。

token一般是客户端登录后服务端生成的令牌，每次访问服务端会进行校验，一般保存到内存即可，也可以放到其他介质；Redis可以做Session共享，如果前端web服务器有几台负载，但是需要保持用户登录的状态，这场景使用比较常见。

我们公司使用oauth+shiro这样的方式来做后台权限的管理，oauth负责多后台统一登录认证，shiro负责给登录用户赋予不同的访问权限。


### [3、SpringBoot、Spring MVC 和 Spring 有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#3springbootspring-mvc-和-spring-有什么区别)  


**1、** Spring

Spring最重要的特征是依赖注入。所有 SpringModules 不是依赖注入就是 IOC 控制反转。

当我们恰当的使用 DI 或者是 IOC 的时候，我们可以开发松耦合应用。松耦合应用的单元测试可以很容易的进行。

**2、** Spring MVC

Spring MVC 提供了一种分离式的方法来开发 Web 应用。通过运用像 DispatcherServelet，MoudlAndView 和 ViewResolver 等一些简单的概念，开发 Web 应用将会变的非常简单。

**3、** SpringBoot

Spring 和 SpringMVC 的问题在于需要配置大量的参数。

SpringBoot 通过一个自动配置和启动的项来目解决这个问题。为了更快的构建产品就绪应用程序，SpringBoot 提供了一些非功能性特征。


### [4、什么是SpringBoot](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#4什么是springboot)  


**1、** 用来简化spring应用的初始搭建以及开发过程 使用特定的方式来进行配置（properties或yml文件）

**2、** 创建独立的spring引用程序 main方法运行

**3、** 嵌入的Tomcat 无需部署war文件

**4、** 简化maven配置


### [5、开启 SpringBoot 特性有哪几种方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#5开启-springboot-特性有哪几种方式)  


**1、** 继承spring-boot-starter-parent项目

**2、** 导入spring-boot-dependencies项目依赖


### [6、什么是YAML?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#6什么是yaml)  


YAML是一种人类可读的数据序列化语言。它通常用于`配置文件`。 与属性文件相比，如果我们想要在配置文件中添加复杂的属性，YAML文件就更加结构化，而且更少混淆。可以看出YAML具有`分层配置数据`。


### [7、什么是Spring Profiles？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#7什么是spring-profiles)  


Spring Profiles允许用户根据配置文件（dev，test，prod等）来注册bean。因此，当应用程序在开发中运行时，只有某些bean可以加载，而在PRODUCTION中，某些其他bean可以加载。假设我们的要求是Swagger文档仅适用于QA环境，并且禁用所有其他文档。这可以使用配置文件来完成。SpringBoot使得使用配置文件非常简单。


### [8、如何在 SpringBoot 中添加通用的 JS 代码？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#8如何在-springboot-中添加通用的-js-代码)  


在源文件夹下，创建一个名为 static 的文件夹。然后，你可以把你的静态的内容放在这里面。

例如，myapp.js 的路径是 resources\static\js\myapp.js

**

你可以参考它在 jsp 中的使用方法：**

错误：HAL browser gives me unauthorized error - Full authenticaition is required to access this resource.

该如何来修复这个错误呢？

两种方法：

方法 1：关闭安全验证

application.properties

```
management.security.enabled:FALSE
```

方法二：在日志中搜索密码并传递至请求标头中


### [9、SpringBoot 有哪几种读取配置的方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#9springboot-有哪几种读取配置的方式)  


SpringBoot 可以通过 @PropertySource,@Value,@Environment, @ConfigurationProperties 来绑定变量。


### [10、SpringBoot 是否可以使用 XML 配置 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新2021年面试题及答案，汇总版.md#10springboot-是否可以使用-xml-配置-)  


SpringBoot 推荐使用 Java 配置而非 XML 配置，但是 SpringBoot 中也可以使用 XML 配置，通过 [@ImportResource ](/ImportResource ) 注解可以引入一个 XML 配置。


### 11、如何重新加载 SpringBoot 上的更改，而无需重新启动服务器？SpringBoot项目如何热部署？
### 12、什么是 Spring Batch？
### 13、什么是 Spring Data REST?
### 14、什么是 JavaConfig？
### 15、什么是SpringBoot？
### 16、我们如何连接一个像 MySQL 或者Orcale 一样的外部数据库？
### 17、SpringBoot中的监视器是什么?
### 18、SpringBoot有哪些优点？
### 19、保护 SpringBoot 应用有哪些方法？
### 20、创建一个 SpringBoot Project 的最简单的方法是什么？
### 21、如何在自定义端口上运行 SpringBoot 应用程序？
### 22、什么是YAML？
### 23、SpringBoot 如何设置支持跨域请求？
### 24、SpringBoot 打成的 jar 和普通的 jar 有什么区别 ?
### 25、SpringBoot 配置文件的加载顺序
### 26、SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？
### 27、SpringBoot 支持哪些日志框架？推荐和默认的日志框架是哪个？
### 28、如何使用 SpringBoot 实现分页和排序？
### 29、Springboot 有哪些优点？
### 30、SpringBoot 有哪些优点？
### 31、SpringBoot性能如何优化





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




