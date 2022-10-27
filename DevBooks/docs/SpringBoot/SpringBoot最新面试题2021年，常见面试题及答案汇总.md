# SpringBoot最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是 SpringBoot Stater ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#1什么是-springboot-stater-)  


启动器是一套方便的依赖没描述符，它可以放在自己的程序中。你可以一站式的获取你所需要的 Spring 和相关技术，而不需要依赖描述符的通过示例代码搜索和复制黏贴的负载。

例如，如果你想使用 Sping 和 JPA 访问数据库，只需要你的项目包含 spring-boot-starter-data-jpa 依赖项，你就可以完美进行。


### [2、SpringBoot多数据源事务如何管理](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#2springboot多数据源事务如何管理)  


第一种方式是在service层的@TransactionManager中使用transactionManager指定DataSourceConfig中配置的事务

第二种是使用jta-atomikos实现分布式事务管理


### [3、SpringBoot 中的 starter 到底是什么 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#3springboot-中的-starter-到底是什么-)  


首先，这个 Starter 并非什么新的技术点，基本上还是基于 Spring 已有功能来实现的。首先它提供了一个自动化配置类，一般命名为 XXXAutoConfiguration ，在这个配置类中通过条件注解来决定一个配置是否生效（条件注解就是 Spring 中原本就有的），然后它还会提供一系列的默认配置，也允许开发者根据实际情况自定义相关配置，然后通过类型安全的属性注入将这些配置属性注入进来，新注入的属性会代替掉默认属性。正因为如此，很多第三方框架，我们只需要引入依赖就可以直接使用了。当然，开发者也可以自定义 Starter


### [4、SpringBoot 有哪几种读取配置的方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#4springboot-有哪几种读取配置的方式)  


SpringBoot 可以通过 @PropertySource,@Value,@Environment, @ConfigurationProperties 来绑定变量


### [5、SpringBoot 支持哪些日志框架？推荐和默认的日志框架是哪个？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#5springboot-支持哪些日志框架推荐和默认的日志框架是哪个)  


SpringBoot 支持 Java Util Logging, Log4j2, Lockback 作为日志框架，如果你使用 Starters 启动器，SpringBoot 将使用 Logback 作为默认日志框架.


### [6、spring boot扫描流程?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#6spring-boot扫描流程)  


**1、** 调用run方法中的`refreshContext`方法

**2、** 用AbstractApplicationContext中的`refresh`方法

**3、** 委托给`invokeBeanFactoryPostProcessors`去处理调用链

**4、** 其中一个方法`postProcessBeanDefinitionRegistry会`去调用`processConfigBeanDefinitions`解析`beandefinitions`

**5、** 在`processConfigBeanDefinitions`中有一个`parse`方法，其中有`componentScanParser.parse`的方法，这个方法会扫描当前路径下所有`Component`组件


### [7、什么是SpringBoot？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#7什么是springboot)  


用来简化spring应用的初始搭建以及开发过程，使用特定的方式来进行配置（`properties`或`yml`文件）创建独立的spring引用程序 main方法运行，嵌入的Tomcat 无需部署war文件，简化maven配置，自动配置spring添加对应功能starter自动化配置


### [8、SpringBoot 支持哪些日志框架？推荐和默认的日志框架是哪个？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#8springboot-支持哪些日志框架推荐和默认的日志框架是哪个)  


SpringBoot 支持 Java Util Logging, Log4j2, Lockback 作为日志框架，如果你使用 Starters 启动器，SpringBoot 将使用 Logback 作为默认日志框架，但是不管是那种日志框架他都支持将配置文件输出到控制台或者文件中。


### [9、如何重新加载SpringBoot上的更改，而无需重新启动服务器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#9如何重新加载springboot上的更改而无需重新启动服务器)  


这可以使用DEV工具来实现。通过这种依赖关系，您可以节省任何更改，嵌入式tomcat将重新启动。SpringBoot有一个开发工具（DevTools）模块，它有助于提高开发人员的生产力。Java开发人员面临的一个主要挑战是将文件更改自动部署到服务器并自动重启服务器。开发人员可以重新加载SpringBoot上的更改，而无需重新启动服务器。这将消除每次手动部署更改的需要。SpringBoot在发布它的第一个版本时没有这个功能。这是开发人员最需要的功能。DevTools模块完全满足开发人员的需求。该模块将在生产环境中被禁用。它还提供H2数据库控制台以更好地测试应用程序。

```
<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-devtools</artifactId>
<optional>true</optional>
```


### [10、什么是 YAML？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringBoot/SpringBoot最新面试题2021年，常见面试题及答案汇总.md#10什么是-yaml)  


YAML 是一种人类可读的数据序列化语言。它通常用于配置文件。与属性文件相比，如果我们想要在配置文件中添加复杂的属性，YAML 文件就更加结构化，而且更少混淆。可以看出 YAML 具有分层配置数据。


### 11、为什么我们需要 spring-boot-maven-plugin?
### 12、如何使用 SpringBoot 生成一个 WAR 文件？
### 13、运行 SpringBoot 有哪几种方式？
### 14、JPA 和 Hibernate 有哪些区别？
### 15、当 SpringBoot 应用程序作为 Java 应用程序运行时，后台会发生什么？
### 16、你如何理解 SpringBoot 配置加载顺序？
### 17、SpringBoot 自动配置原理是什么？
### 18、SpringBoot、Spring MVC 和 Spring 有什么区别
### 19、如何在SpringBoot中禁用Actuator端点安全性？
### 20、你能否举一个以 ReadOnly 为事务管理的例子？
### 21、spring boot监听器流程?
### 22、如何使用SpringBoot实现分页和排序？
### 23、SpringBoot常用的starter有哪些？
### 24、为什么我们不建议在实际的应用程序中使用 Spring Data Rest?
### 25、SpringBoot支持什么前端模板，
### 26、spring-boot-starter-parent 有什么用 ?
### 27、SpringBoot 自动配置原理
### 28、什么是 JavaConfig？
### 29、保护 SpringBoot 应用有哪些方法？
### 30、什么是 Spring Batch?
### 31、spring boot 核心配置文件是什么？bootstrap.properties 和 application.properties 有何区别 ?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




