# Dubbo最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Dubbo集群提供了哪些负载均衡策略？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#1dubbo集群提供了哪些负载均衡策略)  


**1、** Random LoadBalance: 随机选取提供者策略，有利于动态调整提供者权重。截面碰撞率高，调用次数越多，分布越均匀。

**2、** RoundRobin LoadBalance: 轮循选取提供者策略，平均分布，但是存在请求累积的问题。

**3、** LeastActive LoadBalance: 最少活跃调用策略，解决慢提供者接收更少的请求。

**4、** ConstantHash LoadBalance: 一致性 Hash 策略，使相同参数请求总是发到同一提供者，一台机器宕机，可以基于虚拟节点，分摊至其他提供者，避免引起提供者的剧烈变动。

默认为 Random 随机调用。


### [2、Dubbo 服务器注册与发现的流程？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#2dubbo-服务器注册与发现的流程)  


**1、** Provider（提供者）绑定指定端口并启动服务。

**2、** 提供者连接注册中心，并发本机 IP、端口、应用信息和提供服务信息发送至注册中心存储。

**3、** Consumer（消费者），连接注册中心 ，并发送应用信息、所求服务信息至注册中心。

**4、** 注册中心根据消费者所求服务信息匹配对应的提供者列表发送至 Consumer 应用缓存。

**5、** Consumer 在发起远程调用时基于缓存的消费者列表择其一发起调用。

**6、** Provider 状态变更会实时通知注册中心、在由注册中心实时推送至 Consumer。


### [3、同一个服务多个注册的情况下可以直连某一个服务吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#3同一个服务多个注册的情况下可以直连某一个服务吗)  


可以直连，修改配置即可，也可以通过 telnet 直接某个服务。


### [4、默认使用什么序列化框架，你知道的还有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#4默认使用什么序列化框架你知道的还有哪些)  


默认使用Hessian序列化，还有Duddo、FastJson、Java自带序列化。


### [5、你还了解别的分布式框架吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#5你还了解别的分布式框架吗)  


别的还有 spring 的 spring cloud，facebook 的 thrift，twitter 的 finagle 等。冲上云霄，Dubbo Go！GO语言版本都发布了～推荐阅读：Spring Cloud是什么，和Dubbo对比呢？


### [6、Dubbo 的使用场景有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#6dubbo-的使用场景有哪些)  


**1、** 透明化的远程方法调用：就像调用本地方法一样调用远程方法，只需简单配置，没有任何API侵入。

**2、** 软负载均衡及容错机制：可在内网替代 F5 等硬件负载均衡器，降低成本，减少单点。

**3、** 服务自动注册与发现：不再需要写死服务提供方地址，注册中心基于接口名查询服务提供者的IP地址，并且能够平滑添加或删除服务提供者。


### [7、Dubbo 的注册中心集群挂掉，者和订阅者之间还能通信么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#7dubbo-的注册中心集群挂掉者和订阅者之间还能通信么)  


可以的，启动 dubbo 时，消费者会从 zookeeper 拉取注册的生产者的地址接口等数据，缓存在本地。

每次调用时，按照本地存储的地址进行调用。


### [8、同一个服务多个注册的情况下可以直连某一个服务吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#8同一个服务多个注册的情况下可以直连某一个服务吗)  


可以点对点直连，修改配置即可，也可以通过telnet直连某个服务。


### [9、默认使用什么序列化框架，你知道的还有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#9默认使用什么序列化框架你知道的还有哪些)  


推荐使用Hessian序列化，还有Dubbo、FastJson、Java自带序列化。


### [10、Dubbo 和 Dubbox 之间的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Dubbo/Dubbo最新面试题2021年，常见面试题及答案汇总.md#10dubbo-和-dubbox-之间的区别)  


dubbox 基于 dubbo 上做了一些扩展，如加了服务可 restful 调用，更新了开源组件等。


### 11、RPC使用了哪些关键技术，服务调用
### 12、RPC使用了哪些关键技术，RMI
### 13、RPC使用了哪些关键技术，从服务提供者的角度看：
### 14、服务提供者能实现失效踢出是什么原理？
### 15、RPC使用了哪些关键技术，Hessian
### 16、默认使用的是什么通信框架，还有别的选择吗?
### 17、RPC使用了哪些关键技术，服务注册中心
### 18、Dubbo有哪几种负载均衡策略，默认是哪种？
### 19、RPC使用了哪些关键技术，主流RPC框架有哪些
### 20、一般使用什么注册中心？还有别的选择吗？
### 21、RPC使用了哪些关键技术，RPC的实现原理架构图
### 22、Dubbo的管理控制台能做什么？
### 23、Dubbo 在安全方面有哪些措施？
### 24、Dubbo 支持哪些协议，它们的优缺点有哪些？
### 25、你还了解别的分布式框架吗？
### 26、Dubbo 超时设置有哪些方式？
### 27、dubbo能做什么
### 28、Dubbo 的集群容错方案有哪些？
### 29、默认使用什么序列化框架，你知道的还有哪些？
### 30、Dubbo有哪几种集群容错方案，默认是哪种？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




