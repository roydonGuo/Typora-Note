# Dubbo最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Dubbo 是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#1dubbo-是什么)  


Dubbo 是一个分布式、高性能、透明化的 RPC 服务框架，提供服务自动注册、自动发现等高效服务治理方案， 可以和Spring 框架无缝集成


### [2、Dubbo 核心组件有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#2dubbo-核心组件有哪些)  


**1、** Provider：暴露服务的服务提供方

**2、** Consumer：调用远程服务消费方

**3、** Registry：服务注册与发现注册中心

**4、** Monitor：监控中心和访问调用统计

**5、** Container：服务运行容器


### [3、说说核心的配置有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#3说说核心的配置有哪些)  


核心配置有：

**1、** dubbo:service/

**2、** dubbo:reference/

**3、** dubbo:protocol/

**4、** dubbo:registry/

**5、** dubbo:application/

**6、** dubbo:provider/

**7、** dubbo:consumer/

**8、** dubbo:method/


### [4、什么是RPC](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#4什么是rpc)  


RPC（Remote Procedure Call Protocol）远程过程调用协议，它是一种通过网络从远程计算机程序上请求服务，而不需要了解底层网络技术的协议。简言之，RPC使得程序能够像访问本地系统资源一样，去访问远端系统资源。比较关键的一些方面包括：通讯协议、序列化、资源（接口）描述、服务框架、性能、语言支持等。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/026/54/80_3.png#alt=80%5C_3.png)

简单的说，RPC就是从一台机器(客户端)上通过参数传递的方式调用另一台机器(服务器)上的一个函数或方法(可以统称为服务)并得到返回的结果。


### [5、RPC使用了哪些关键技术，Thrift](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#5rpc使用了哪些关键技术thrift)  


是一种可伸缩的跨语言服务的软件框架。它拥有功能强大的代码生成引擎，无缝地支持C + +，C#，Java，Python和PHP和Ruby。thrift允许你定义一个描述文件，描述数据类型和服务接口。依据该文件，编译器方便地生成RPC客户端和服务器通信代码。

最初由facebook开发用做系统内个语言之间的RPC通信，2007年由facebook贡献到apache基金 ，现在是apache下的opensource之一 。支持多种语言之间的RPC方式的通信：php语言client可以构造一个对象，调用相应的服务方法来调用java语言的服务，跨越语言的C/S RPC调用。底层通讯基于SOCKET。


### [6、服务读写推荐的容错策略是怎样的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#6服务读写推荐的容错策略是怎样的)  


读操作建议使用 Failover 失败自动切换，默认重试两次其他服务器。写操作建议使用 Failfast 快速失败，发一次调用失败就立即报错。


### [7、Dubbo 的默认集群容错方案？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#7dubbo-的默认集群容错方案)  


Failover Cluster


### [8、当一个服务接口有多种实现时怎么做？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#8当一个服务接口有多种实现时怎么做)  


当一个接口有多种实现时，可以用 group 属性来分组，服务提供方和消费方都指定同一个 group 即可。


### [9、服务调用超时问题怎么解决？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#9服务调用超时问题怎么解决)  


dubbo 在调用服务不成功时，默认是会重试两次的。


### [10、同一个服务多个注册的情况下可以直连某一个服务吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新2021年面试题附答案解析，大汇总.md#10同一个服务多个注册的情况下可以直连某一个服务吗)  


可以点对点直连，修改配置即可，也可以通过 telnet 直接某个服务。


### 11、Dubbo 用到哪些设计模式？
### 12、Dubbo 和 Spring Cloud 有什么关系？
### 13、dubbo和dubbox之间的区别？
### 14、默认使用什么序列化框架，你知道的还有哪些？
### 15、Dubbo 使用的是什么通信框架?
### 16、说说核心的配置有哪些？
### 17、如何解决服务调用链过长的问题？
### 18、Dubbo 支持服务降级吗？
### 19、RPC使用了哪些关键技术，服务寻址
### 20、服务上线怎么兼容旧版本？
### 21、Dubbo 必须依赖的包有哪些？
### 22、在使用过程中都遇到了些什么问题？ 如何解决的？
### 23、为什么要有RPC
### 24、Dubbo服务之间的调用是阻塞的吗？
### 25、Dubbo 和 Spring Cloud 的区别？
### 26、Dubbo 在安全机制方面是如何解决的
### 27、RPC使用了哪些关键技术，protobuf-rpc-pro
### 28、Dubbo 的整体架构设计有哪些分层?
### 29、服务提供者能实现失效踢出的是什么原理？
### 30、Dubbo 使用过程中都遇到了些什么问题？
### 31、Dubbo 服务器注册与发现的流程？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




