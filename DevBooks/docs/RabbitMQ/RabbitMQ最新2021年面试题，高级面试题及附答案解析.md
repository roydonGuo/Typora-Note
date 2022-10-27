# RabbitMQ最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、vhost 是什么？起什么作用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#1vhost-是什么起什么作用)  


vhost 可以理解为虚拟 broker ，即 mini-RabbitMQ server。其内部均含有独立的queue、exchange 和 binding 等，但最最重要的是，其拥有独立的权限系统，可以做到vhost 范围的用户控制。

当然，从 RabbitMQ 的全局角度，vhost 可以作为不同权限隔离的手段（一个典型的例子就是不同的应用可以跑在不同的 vhost 中）。


### [2、AMQP协议3层？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#2amqp协议3层)  


**1、** Module Layer：协议最高层，主要定义了一些客户端调用的命令，客户端可以用这些命令实现自己的业务逻辑。

**2、** Session Layer：中间层，主要负责客户端命令发送给服务器，再将服务端应答返回客户端，提供可靠性同步机制和错误处理。

**3、** TransportLayer：最底层，主要传输二进制数据流，提供帧的处理、信道服用、错误检测和数据表示等。


### [3、RabbitMQ topic 主题模式(路由模式的一种)](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#3rabbitmq-topic-主题模式路由模式的一种)  


![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/030/5/35_8.png#alt=35%5C_8.png)

**1、** 星号井号代表通配符

**2、** 星号代表多个单词,井号代表一个单词

**3、** 路由功能添加模糊匹配

**4、** 消息产生者产生消息,把消息交给交换机

**5、** 交换机根据key的规则模糊匹配到对应的队列,由队列的监听消费者接收消息消费

在我的理解看来就是routing查询的一种模糊匹配，就类似sql的模糊查询方式


### [4、RabbitMQ基本概念](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#4rabbitmq基本概念)  


**1、** Broker： 简单来说就是消息队列服务器实体

**2、** Exchange： 消息交换机，它指定消息按什么规则，路由到哪个队列

**3、** Queue： 消息队列载体，每个消息都会被投入到一个或多个队列

**4、** Binding： 绑定，它的作用就是把exchange和queue按照路由规则绑定起来

**5、** Routing Key： 路由关键字，exchange根据这个关键字进行消息投递

**6、** VHost： vhost 可以理解为虚拟 broker ，即 mini-RabbitMQ server。其内部均含有独立的 queue、exchange 和 binding 等，但最最重要的是，其拥有独立的权限系统，可以做到 vhost 范围的用户控制。当然，从 RabbitMQ 的全局角度，vhost 可以作为不同权限隔离的手段（一个典型的例子就是不同的应用可以跑在不同的 vhost 中）。

**7、** Producer： 消息生产者，就是投递消息的程序

**8、** Consumer： 消息消费者，就是接受消息的程序

**9、** Channel： 消息通道，在客户端的每个连接里，可建立多个channel，每个channel代表一个会话任务

由Exchange、Queue、RoutingKey三个才能决定一个从Exchange到Queue的唯一的线路。


### [5、消息如何被优先消费？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#5消息如何被优先消费)  


生产者

```
Map<String, Object> argss = new HashMap<String, Object>();
argss.put("x-max-priority",10);
```

消费者

```
AMQP.BasicProperties properties = new AMQP.BasicProperties.Builder()
    .priority(5) // 优先级，默认为5，配合队列的 x-max-priority 属性使用
```


### [6、在单 node 系统和多 node 构成的 cluster 系统中声明 queue、exchange ，以及进行 binding 会有什么不同？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#6在单-node-系统和多-node-构成的-cluster-系统中声明-queueexchange-以及进行-binding-会有什么不同)  


当你在单 node 上声明 queue 时，只要该 node 上相关元数据进行了变更，你就会得到 Queue.Declare-ok 回应；而在 cluster 上声明 queue ，则要求 cluster 上的全部node 都要进行元数据成功更新，才会得到 Queue.Declare-ok 回应。

另外，若 node 类型为 RAM node 则变更的数据仅保存在内存中，若类型为 disk node 则还要变更保存在磁盘上的数据。


### [7、RabbitMQ消息是如何路由的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#7rabbitmq消息是如何路由的)  


**消息路由必须有三部分：交换器、路由、绑定。**

生产者把消息发布到交换器上，绑定决定了消息如何从路由器路由到特定的队列；消息最终到达队列，并被消费者接收。

1. 消息发布到交换器时，消息将拥有一个 路由键（routing key） ， 在消息创建时设定。
2. 通过队列路由键，可以把队列绑定到交换器上。
3. 消息到达交换器后，RabbitMQ会将消息的路由键与队列的路由键进行匹配（针对不同的交换器有不同的路由规则）。如果能够匹配到队列，则消息会投递到相应队列中；如果不能匹配到任何队列，消息将进入"黑洞"。

**常用的交换器主要分为以下三种：**

1. direct ：如果路由键完全匹配，消息就会被投递到相应的队列；每个AMQP的实现都必须有一个direct交换器，包含一个空白字符串名称的默认交换器。声明一个队列时，会自动绑定到默认交换器，并且以队列名称作为路由键：channel -> basic_public($msg, '', 'queue-name')
2. fanout ： 如果交换器收到消息，将会广播到所有绑定的队列上；
3. topic ：可以使来自不同源头的消息能够到达同一个队列。使用topic交换器时，可以使用通配符，比如："*" 匹配特定位置的任意文本，"." 把路由键分为了几个标识符， "#" 匹配所有规则等。
4. 特别注意：发往topic交换器的消息不能随意的设置选择键（routing_key），必须是有"."隔开的一系列的标识符组成。


### [8、交换器4种类型？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#8交换器4种类型)  


主要有以下4种。

fanout:把所有发送到该交换器的消息路由到所有与该交换器绑定的队列中。

direct:把消息路由到BindingKey和RoutingKey完全匹配的队列中。

topic:

匹配规则：

RoutingKey 为一个 点号'.': 分隔的字符串。 比如: java.xiaoka.show

BindingKey和RoutingKey一样也是点号“.“分隔的字符串。

BindingKey可使用 _ 和 # 用于做模糊匹配，_匹配一个单词，#匹配多个或者0个

headers:不依赖路由键匹配规则路由消息。是根据发送消息内容中的headers属性进行匹配。性能差，基本用不到。


### [9、交换器无法根据自身类型和路由键找到符合条件队列时，有哪些处理？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#9交换器无法根据自身类型和路由键找到符合条件队列时有哪些处理)  


mandatory ：true 返回消息给生产者。

mandatory: false 直接丢弃。


### [10、RabbitMQ队列结构？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题，高级面试题及附答案解析.md#10rabbitmq队列结构)  


**通常由以下两部分组成：**

rabbit_amqqueue_process：负责协议相关的消息处理，即接收生产者的消息、向消费者交付消息、处理消息的确认(包括生产端的 confirm 和消费端的 ack) 等。

backing_queue：是消息存储的具体形式和引擎，并向 rabbit amqqueue process 提供相关的接口以供调用。


### 11、什么是MQ
### 12、如何保证RabbitMQ消息的顺序性？
### 13、消息基于什么传输？
### 14、RabbitMQ的特点?
### 15、为什么要使用rabbitmq
### 16、AMQP模型的几大组件？
### 17、如何确保消息不丢失？
### 18、RabbitMQ work工作模式(资源的竞争)
### 19、AMQP模型的几大组件？
### 20、使用rabbitmq的场景
### 21、什么是Exchange交换器？
### 22、MQ的优点
### 23、为什么 heavy RPC 的使用场景下不建议采用 disk node ？
### 24、如何保证RabbitMQ不被重复消费？
### 25、如何确保消息正确地发送至RabbitMQ？ 如何确保消息接收方消费了消息？
### 26、RabbitMQ 包括哪些要素？
### 27、设计MQ思路
### 28、RabbitMQ 中的 Broker 是指什么？Cluster 又是指什么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




