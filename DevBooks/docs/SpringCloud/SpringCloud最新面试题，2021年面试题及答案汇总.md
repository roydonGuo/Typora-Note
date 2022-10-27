# SpringCloud最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是Spring引导的执行器？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#1什么是spring引导的执行器)  


SpringBoot执行程序提供了restful Web服务，以访问生产环境中运行应用程序的当前状态。在执行器的帮助下，您可以检查各种指标并监控您的应用程序。


### [2、什么是持续集成（CI）？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#2什么是持续集成ci)  


持续集成（CI）是每次团队成员提交版本控制更改时自动构建和测试代码的过程。这鼓励开发人员通过在每个小任务完成后将更改合并到共享版本控制存储库来共享代码和单元测试。


### [3、你对SpringBoot有什么了解？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#3你对springboot有什么了解)  


事实上，随着新功能的增加，弹簧变得越来越复杂。如果必须启动新的spring项目，则必须添加构建路径或添加maven依赖项，配置应用程序服务器，添加spring配置。所以一切都必须从头开始。

SpringBoot是解决这个问题的方法。使用spring boot可以避免所有样板代码和配置。因此，基本上认为自己就好像你正在烘烤蛋糕一样，春天就像制作蛋糕所需的成分一样，弹簧靴就是你手中的完整蛋糕。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_12.png#alt=img%5C_12.png)

图10：  SpringBoot的因素 – 微服务面试问题


### [4、Ribbon和Feign调用服务的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#4ribbon和feign调用服务的区别)  


**1、** 调用方式同：Ribbon需要我们自己构建Http请求，模拟Http请求然后通过RestTemplate发给其他服务，步骤相当繁琐

**2、** 而Feign则是在Ribbon的基础上进行了一次改进，采用接口的形式，将我们需要调用的服务方法定义成抽象方法保存在本地就可以了，不需要自己构建Http请求了，直接调用接口就行了，不过要注意，调用方法要和本地抽象方法的签名完全一致。


### [5、Spring Cloud和SpringBoot版本对应关系](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#5spring-cloud和springboot版本对应关系)  

| Spring Cloud Version | SpringBoot Version |
| --- | --- |
| Hoxton | 2.2.x |
| Greenwich | 2.1.x |
| Finchley | 2.0.x |
| Edgware | 1.5.x |
| Dalston | 1.5.x |



### [6、微服务有哪些特点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#6微服务有哪些特点)  


![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0816/01/img_3.png#alt=img%5C_3.png)

图3：微服务的 特点 – 微服务访谈问题

解耦 – 系统内的服务很大程度上是分离的。因此，整个应用程序可以轻松构建，更改和扩展

组件化 – 微服务被视为可以轻松更换和升级的独立组件

业务能力 – 微服务非常简单，专注于单一功能

自治 – 开发人员和团队可以彼此独立工作，从而提高速度

持续交付 – 通过软件创建，测试和批准的系统自动化，允许频繁发布软件

责任 – 微服务不关注应用程序作为项目。相反，他们将应用程序视为他们负责的产品

分散治理 – 重点是使用正确的工具来做正确的工作。这意味着没有标准化模式或任何技术模式。开发人员可以自由选择最有用的工具来解决他们的问题

敏捷 – 微服务支持敏捷开发。任何新功能都可以快速开发并再次丢弃


### [7、Ribbon是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#7ribbon是什么)  


**1、** Ribbon是Netflix发布的开源项目，主要功能是提供客户端的软件负载均衡算法

**2、** Ribbon客户端组件提供一系列完善的配置项，如连接超时，重试等。简单的说，就是在配置文件中列出后面所有的机器，Ribbon会自动的帮助你基于某种规则（如简单轮询，随即连接等）去连接这些机器。我们也很容易使用Ribbon实现自定义的负载均衡算法。（有点类似Nginx）


### [8、微服务之间是如何独立通讯的?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#8微服务之间是如何独立通讯的)  


**1、** 远程调用，比如feign调用，直接通过远程过程调用来访问别的service。 2.消息中间件


### [9、什么是网关?](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#9什么是网关)  


网关相当于一个网络服务架构的入口，所有网络请求必须通过网关转发到具体的服务。


### [10、使用Spring Cloud有什么优势？](https://gitee.com/souyunku/DevBooks/blob/master/docs/SpringCloud/SpringCloud最新面试题，2021年面试题及答案汇总.md#10使用spring-cloud有什么优势)  


使用SpringBoot开发分布式微服务时，我们面临以下问题

**1、** 与分布式系统相关的复杂性-这种开销包括网络问题，延迟开销，带宽问题，安全问题。

**2、** 服务发现-服务发现工具管理群集中的流程和服务如何查找和互相交谈。它涉及一个服务目录，在该目录中注册服务，然后能够查找并连接到该目录中的服务。

**3、** 冗余-分布式系统中的冗余问题。

**4、** 负载平衡 --负载平衡改善跨多个计算资源的工作负荷，诸如计算机，计算机集群，网络链路，中央处理单元，或磁盘驱动器的分布。

**5、** 性能-问题 由于各种运营开销导致的性能问题。

**6、** 部署复杂性-Devops技能的要求。


### 11、单片，SOA和微服务架构有什么区别？
### 12、什么是Hystrix断路器？我们需要它吗？
### 13、DiscoveryClient的作用
### 14、微服务限流 http限流：我们使⽤nginx的limitzone来完成：
### 15、Zuul网关如何搭建集群
### 16、使用 SpringBoot 开发分布式微服务时，我们面临什么问题
### 17、如何设置服务发现？
### 18、如何实现动态Zuul网关路由转发
### 19、过渡到微服务时的常见错误
### 20、SpringCloud主要项目
### 21、常用网关框架有那些？
### 22、在微服务中，如何保护服务?
### 23、您将如何在微服务上执行安全测试？
### 24、Docker的目的是什么？
### 25、微服务的优点
### 26、缓存机制：
### 27、如何设计一套API接口
### 28、什么是微服务架构
### 29、什么是双因素身份验证？
### 30、什么是领域驱动设计？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




