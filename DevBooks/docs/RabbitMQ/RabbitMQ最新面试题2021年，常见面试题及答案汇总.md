# RabbitMQ最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、集群中的节点类型？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#1集群中的节点类型)  


内存节点：ram,将变更写入内存。

磁盘节点：disc,磁盘写入操作。

RabbitMQ要求最少有一个磁盘节点。


### [2、集群节点类型有几种？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#2集群节点类型有几种)  


内存节点：保存状态到内存，但持久化的队列和消息还是会保存到磁盘；

磁盘节点：保存状态到内存和磁盘，一个集群中至少需要一个磁盘节点


### [3、Consumer Cancellation Notification 机制用于什么场景？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#3consumer-cancellation-notification-机制用于什么场景)  


用于保证当镜像 queue 中 master 挂掉时，连接到 slave 上的 consumer 可以收到自身 consume 被取消的通知，进而可以重新执行 consume 动作从新选出的 master 出获得消息。若不采用该机制，连接到 slave 上的 consumer 将不会感知 master 挂掉这个事情，导致后续无法再收到新 master 广播出来的 message 。另外，因为在镜像 queue 模式下，存在将 message 进行 requeue 的可能，所以实现 consumer 的逻辑时需要能够正确处理出现重复 message 的情况。


### [4、消息传输保证层级？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#4消息传输保证层级)  


**1、** At most once：最多一次。消息可能会丢失，单不会重复传输。

**2、** At least once：最少一次。消息觉不会丢失，但可能会重复传输。

**3、** Exactly once：恰好一次，每条消息肯定仅传输一次。


### [5、事务机制？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#5事务机制)  


RabbitMQ 客户端中与事务机制相关的方法有三个:

channel.txSelect 用于将当前的信道设置成事务模式。

channel 、txCommit 用于提交事务 。

channel 、txRollback 用于事务回滚,如果在事务提交执行之前由于 RabbitMQ 异常崩溃或者其他原因抛出异常,通过txRollback来回滚。


### [6、如何避免消息重复投递或重复消费?](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#6如何避免消息重复投递或重复消费)  


在消息生产时，MQ内部针对每条生产者发送的消息生成一个`inner-msg-id`，作为去重和幂等的依据（消息投递失败并重传），避免重复的消息进入队列；在消息消费时，要求消息体中必须要有一个`bizId`（对于同一业务全局唯一，如支付ID、订单ID、帖子ID等）作为去重和幂等的依据，避免同一条消息被重复消费。

这个问题针对业务场景来答分以下几点：

**1、** 拿到这个消息做数据库的insert操作。然后给这个消息做一个唯一主键，那么就算出现重复消费的情况，就会导致主键冲突，避免数据库出现脏数据。

**2、** 拿到这个消息做Redis的set的操作，因为你无论set几次结果都是一样的，set操作本来就算幂等操作。

**3、** 如果上面两种情况还不行。准备一个第三方介质,来做消费记录。以Redis为例，给消息分配一个全局id，只要消费过该消息，将<id,message>以K-V形式写入Redis。那消费者开始消费前，先去Redis中查询有没消费记录即可。


### [7、routing_key 和 binding_key 的最大长度是多少？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#7routing_key-和-binding_key-的最大长度是多少)  


255 字节。


### [8、RabbitMQ消息确认过程？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#8rabbitmq消息确认过程)  


1.
消费者收到的每一条消息都必须进行确认（自动确认和自行确认）

2.
消费者在声明队列时，可以置顶autoAck参数，当autoAck = false时，RabbitMQ会等待消费者显式发送回 ack 信号后才从内存（和磁盘，如果是持久化消息的话）中删除消息，否则RabbitMQ会在队列中消息被消费后立即删除它。

3.
采用消息确认机制后，只要使 autoAck = false，消费者就有足够的时间处理消息（任务），不用担心处理消息过程中消费者进程挂掉后消息丢失的问题，因为RabbitMQ会一直持有消息直到消费者显式调用basicAck为止。

4.
当autoAck = false时，对于RabbitMQ服务器端而言，队列中的消息分成了两部分：一部分是等待投递给消费者的消息；一部分是已经投递给消费者，但是还没有收到消费者ack信号的消息。如果服务器端一直没有收到消费者的ack信号，并且消费此消息的消费者已经断开连接，则服务器端会安排该消息 重新进入队列，等待投递给下一个消费者（也可能还是原来的那个消费者）。

5.
RabbitMQ不会为 ack消息设置超时时间，它判断此消息是否需要重新投递给消费者的唯一依据是消费该消息的消费者连接是否已经断开。这么设计的原因是RabbitMQ允许消费者消费一条消息的时间可以很久很久。



### [9、RabbitMQ如何实现延时队列?](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#9rabbitmq如何实现延时队列)  


利用TTL（队列的消息存活时间或者消息存活时间），加上死信交换机

```
// 设置属性，消息10秒钟过期
AMQP.BasicProperties properties = new AMQP.BasicProperties.Builder()
.expiration("10000") // TTL

// 指定队列的死信交换机
Map<String,Object> arguments = new HashMap<String,Object>();
arguments.put("x-dead-letter-exchange","DLX_EXCHANGE");
```


### [10、消息怎么路由？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新面试题2021年，常见面试题及答案汇总.md#10消息怎么路由)  


从概念上来说，消息路由必须有三部分：交换器、路由、绑定。生产者把消息到交换器上；绑定决定了消息如何从路由器路由到特定的队列；消息最终到达队列，并被消费者接收。

消息到交换器时，消息将拥有一个路由键（routing key），在消息创建时设定。通过队列路由键，可以把队列绑定到交换器上。消息到达交换器后，RabbitMQ会将消息的路由键与队列的路由键进行匹配（针对不同的交换器有不同的路由规则）。如果能够匹配到队列，则消息会投递到相应队列中；如果不能匹配到任何队列，消息将进入 “黑洞”。

**常用的交换器主要分为一下三种：**

**1、** direct：如果路由键完全匹配，消息就被投递到相应的队列

**2、** fanout：如果交换器收到消息，将会广播到所有绑定的队列上

**3、** topic：可以使来自不同源头的消息能够到达同一个队列。使用topic交换器时，可以使用通配符。比如：“*” 匹配特定位置的任意文本， “.” 把路由键分为了几部分，“#” 匹配所有规则等。特别注意：发往topic交换器的消息不能随意的设置选择键（routing_key），必须是由"."隔开的一系列的标识符组成。


### 11、为什么不应该对所有的 message 都使用持久化机制？
### 12、生产者Producer?
### 13、解耦、异步、削峰是什么？。
### 14、什么是生产者Producer?
### 15、cluster 中 node 的失效会对 consumer 产生什么影响？若是在 cluster 中创建了mirrored queue ，这时 node 失效会对 consumer 产生什么影响？
### 16、消息如何分发?
### 17、如何保证高可用的？RabbitMQ 的集群
### 18、多个消费者监听一个队列时，消息如何分发?
### 19、客户端连接到 cluster 中的任意 node 上是否都能正常工作？
### 20、消费者接收消息过程？
### 21、消费者某些原因无法处理当前接受的消息如何来拒绝？
### 22、如何避免消息重复投递或重复消费？
### 23、RabbitMQ simple模式（即最简单的收发模式）
### 24、rabbitmq 的使用场景
### 25、RabbitMQ概念里的channel、exchange 和 queue是逻辑概念，还是对应着进程实体？作用分别是什么？
### 26、消费者接收消息过程？
### 27、RabbitMQ 上的一个 queue 中存放的 message 是否有数量限制？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




