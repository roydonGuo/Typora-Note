# RabbitMQ最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、死信队列和延迟队列的使用?](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#1死信队列和延迟队列的使用)  


**1、** 死信消息：消息被拒绝（Basic.Reject或Basic.Nack）并且设置 requeue 参数的值为 false 消息过期了 队列达到最大的长度

**2、** 过期消息：在 rabbitmq 中存在2种方可设置消息的过期时间，第一种通过对队列进行设置，这种设置后，该队列中所有的消息都存在相同的过期时间，第二种通过对消息本身进行设置，那么每条消息的过期时间都不一样。如果同时使用这2种方法，那么以过期时间小的那个数值为准。当消息达到过期时间还没有被消费，那么那个消息就成为了一个 死信 消息。

**3、** 队列设置：在队列申明的时候使用 x-message-ttl 参数，单位为 毫秒

**4、** 单个消息设置：是设置消息属性的 expiration 参数的值，单位为 毫秒

**5、** 延时队列：在rabbitmq中不存在延时队列，但是我们可以通过设置消息的过期时间和死信队列来模拟出延时队列。消费者监听死信交换器绑定的队列，而不要监听消息发送的队列。

场景演示：需求：用户在系统中创建一个订单，如果超过时间用户没有进行支付，那么自动取消订单。

**分析：**

**1、** 上面这个情况，我们就适合使用延时队列来实现，那么延时队列如何创建

**2、** 延时队列可以由 过期消息+死信队列 来时间

**3、** 过期消息通过队列中设置 x-message-ttl 参数实现

**4、** 死信队列通过在队列申明时，给队列设置 x-dead-letter-exchange 参数，然后另外申明一个队列绑定x-dead-letter-exchange对应的交换器。

```
ConnectionFactory factory = new ConnectionFactory(); 
factory.setHost("127.0.0.1"); 
factory.setPort(AMQP.PROTOCOL.PORT); 
factory.setUsername("guest"); 
factory.setPassword("guest"); 
Connection connection = factory.newConnection(); 
Channel channel = connection.createChannel();
// 
// 声明一个接收被删除的消息的交换机和队列 
String EXCHANGE_DEAD_NAME = "exchange.dead"; 
String QUEUE_DEAD_NAME = "queue_dead"; 
channel.exchangeDeclare(EXCHANGE_DEAD_NAME, BuiltinExchangeType.DIRECT); 
channel.queueDeclare(QUEUE_DEAD_NAME, false, false, false, null); 
channel.queueBind(QUEUE_DEAD_NAME, EXCHANGE_DEAD_NAME, "routingkey.dead"); 
// 
String EXCHANGE_NAME = "exchange.fanout"; 
String QUEUE_NAME = "queue_name"; 
channel.exchangeDeclare(EXCHANGE_NAME, BuiltinExchangeType.FANOUT); 
Map<String, Object> arguments = new HashMap<String, Object>(); 
// 统一设置队列中的所有消息的过期时间 
arguments.put("x-message-ttl", 30000); 
// 设置超过多少毫秒没有消费者来访问队列，就删除队列的时间 
arguments.put("x-expires", 20000); 
// 设置队列的最新的N条消息，如果超过N条，前面的消息将从队列中移除掉 
arguments.put("x-max-length", 4); 
// 设置队列的内容的最大空间，超过该阈值就删除之前的消息
arguments.put("x-max-length-bytes", 1024); 
// 将删除的消息推送到指定的交换机，一般x-dead-letter-exchange和x-dead-letter-routing-key需要同时设置
arguments.put("x-dead-letter-exchange", "exchange.dead"); 
// 将删除的消息推送到指定的交换机对应的路由键 
arguments.put("x-dead-letter-routing-key", "routingkey.dead"); 
// 设置消息的优先级，优先级大的优先被消费 
arguments.put("x-max-priority", 10); 
channel.queueDeclare(QUEUE_NAME, false, false, false, arguments); 
channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, ""); 
String message = "Hello RabbitMQ: "; 
// 
for(int i = 1; i <= 5; i++) { 
 // expiration: 设置单条消息的过期时间 
 AMQP.BasicProperties.Builder properties = new AMQP.BasicProperties().builder().priority(i).expiration( i * 1000 + ""); 
 channel.basicPublish(EXCHANGE_NAME, "", properties.build(), (message + i).getBytes("UTF-8")); 
} 
channel.close(); 
connection.close();
```


### [2、RabbitMQ的集群模式有几种？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#2rabbitmq的集群模式有几种)  


RabbitMQ 是比较有代表性的，因为是基于主从（非分布式）做高可用性的，我们就以 RabbitMQ 为例子讲解第一种 MQ 的高可用性怎么实现。RabbitMQ 有三种模式：`单机模式`、`普通集群模式`、`镜像集群模式`。

**1、** 单机模式，就是 Demo 级别的，一般就是你本地启动了玩玩儿的?，没人生产用单机模式

**2、** 普通模式：以两个节点（rabbit01，rabbit02）为例来进行说明，对于Queue来说，消息实体只存在于其中一个节点rabbit01（或者rabbit02），rabbit01和rabbit02两个节点仅有相同的元数据，即队列结构。当消息进入rabbit01节点的Queue后，consumer从rabbit02节点消费时，RabbitMQ会临时在rabbit01，rabbit02间进行消息传输，把A中的消息实体取出并经过B发送给consumer，所以consumer应尽量连接每一个节点，从中取消息。即对于同一个逻辑队列，要在多个节点建立物理Queue。否则无论consumer连rabbit01或rabbit02，出口总在rabbit01，会产生瓶颈。当rabbit01节点故障后，rabbit02节点无法取到rabbit01节点中还未消费的消息实体。如果做了消息持久化，那么等到rabbit01节点恢复，然后才可被消费。如果没有消息持久化，就会产生消息丢失的现象。

**3、** 镜像模式：把需要的队列做成镜像队列，存在与多个节点属于RabibitMQ的HA方案，该模式解决了普通模式中的问题，其实质和普通模式不同之处在于，消息体会主动在镜像节点间同步，而不是在客户端取数据时临时拉取，该模式带来的副作用也很明显，除了降低系统性能外，如果镜像队列数量过多，加之大量的消息进入，集群内部的网络带宽将会被这种同步通讯大大消耗掉，所以在对可靠性要求比较高的场合中适用


### [3、无法被路由的消息去了哪里?](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#3无法被路由的消息去了哪里)  


mandatory：true 返回消息给生产者。

mandatory：false 直接丢弃。


### [4、向不存在的 exchange 发 publish 消息会发生什么？向不存在的 queue 执行consume 动作会发生什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#4向不存在的-exchange-发-publish-消息会发生什么向不存在的-queue-执行consume-动作会发生什么)  


都会收到 Channel.Close 信令告之不存在（内含原因 404 NOT_FOUND）。


### [5、消息如何保证幂等性？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#5消息如何保证幂等性)  


生产者方面：可以对每条消息生成一个msgID，以控制消息重复投递

```
AMQP.BasicProperties properties = new AMQP.BasicProperties.Builder()
porperties.messageId(String.valueOF(UUID.randomUUID()))
```

消费者方面：消息体中必须携带一个业务ID，如银行流水号，消费者可以根据业务ID去重，避免重复消费


### [6、生产者消息如何运转？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#6生产者消息如何运转)  


**1、** Producer先连接到Broker,建立连接Connection,开启一个信道(Channel)。

**2、** Producer声明一个交换器并设置好相关属性。

**3、** Producer声明一个队列并设置好相关属性。

**4、** Producer通过路由键将交换器和队列绑定起来。

**5、** Producer发送消息到Broker,其中包含路由键、交换器等信息。

**6、** 相应的交换器根据接收到的路由键查找匹配的队列。

**7、** 如果找到，将消息存入对应的队列，如果没有找到，会根据生产者的配置丢弃或者退回给生产者。

**8、** 关闭信道。

**9、** 管理连接。


### [7、优先级队列？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#7优先级队列)  


优先级高的队列会先被消费。

可以通过x-max-priority参数来实现。

当消费速度大于生产速度且Broker没有堆积的情况下，优先级显得没有意义。


### [8、消费者某些原因无法处理当前接受的消息如何来拒绝？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#8消费者某些原因无法处理当前接受的消息如何来拒绝)  


channel.basicNack

channel.basicReject


### [9、消息基于什么传输?](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#9消息基于什么传输)  


由于TCP连接的创建和销毁开销较大，且并发数受系统资源限制，会造成性能瓶颈。RabbitMQ使用信道的方式来传输数据。信道是建立在真实的TCP连接内的虚拟连接，且每条TCP连接上的信道数量没有限制。


### [10、rabbitmq的集群](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题，2021年面试题及答案汇总.md#10rabbitmq的集群)  


**镜像集群模式**

你创建的queue，无论元数据还是queue里的消息都会存在于多个实例上，然后每次你写消息到queue的时候，都会自动把消息到多个实例的queue里进行消息同步。

好处在于，你任何一个机器宕机了，没事儿，别的机器都可以用。坏处在于，第一，这个性能开销也太大了吧，消息同步所有机器，导致网络带宽压力和消耗很重！第二，这么玩儿，就没有扩展性可言了，如果某个queue负载很重，你加机器，新增的机器也包含了这个queue的所有数据，并没有办法线性扩展你的queue


### 11、RabbitMQ事务机制？
### 12、RoutingKey路由键？
### 13、如何确保消息正确地发送至RabbitMQ?
### 14、RabbitMQ中消息可能有的几种状态?
### 15、发送确认机制？
### 16、什么是RabbitMQ？
### 17、Queue队列？
### 18、RabbitMQ中消息可能有的几种状态?
### 19、RabbitMQ的工作模式有几种？
### 20、队列结构？
### 21、消费者Consumer?
### 22、什么是元数据？元数据分为哪些类型？包括哪些内容？与 cluster 相关的元数据有哪些？元数据是如何保存的？元数据在 cluster 中是如何分布的？
### 23、vhost 是什么? 起什么作用?
### 24、你们公司生产环境用的是什么消息中间件？
### 25、什么是Broker服务节点？
### 26、什么情况下 producer 不主动创建 queue 是安全的？
### 27、MQ 有哪些常见问题？如何解决这些问题？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




