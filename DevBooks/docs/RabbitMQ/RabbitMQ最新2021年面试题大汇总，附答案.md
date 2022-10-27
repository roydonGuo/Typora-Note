# RabbitMQ最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、如何解决消息队列的延时以及过期失效问题？消息队列满了以后该怎么处理？有几百万消息持续积压几小时，怎么办？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#1如何解决消息队列的延时以及过期失效问题消息队列满了以后该怎么处理有几百万消息持续积压几小时怎么办)  


**消息积压处理办法：临时紧急扩容：**

**1、** 先修复 consumer 的问题，确保其恢复消费速度，然后将现有 cnosumer 都停掉。

**2、** 新建一个 topic，partition 是原来的 10 倍，临时建立好原先 10 倍的 queue 数量。

**3、** 然后写一个临时的分发数据的 consumer 程序，这个程序部署上去消费积压的数据，消费之后不做耗时的处理，直接均匀轮询写入临时建立好的 10 倍数量的 queue。

**4、** 接着临时征用 10 倍的机器来部署 consumer，每一批 consumer 消费一个临时 queue 的数据。这种做法相当于是临时将 queue 资源和 consumer 资源扩大 10 倍，以正常的 10 倍速度来消费数据。

**5、** 等快速消费完积压数据之后，得恢复原先部署的架构，重新用原先的 consumer 机器来消费消息。

**6、** MQ中消息失效：假设你用的是 RabbitMQ，RabbtiMQ 是可以设置过期时间的，也就是 TTL。如果消息在 queue 中积压超过一定的时间就会被 RabbitMQ 给清理掉，这个数据就没了。那这就是第二个坑了。这就不是说数据会大量积压在 mq 里，而是大量的数据会直接搞丢。我们可以采取一个方案，就是批量重导，这个我们之前线上也有类似的场景干过。就是大量积压的时候，我们当时就直接丢弃数据了，然后等过了高峰期以后，比如大家一起喝咖啡熬夜到晚上12点以后，用户都睡觉了。这个时候我们就开始写程序，将丢失的那批数据，写个临时程序，一点一点的查出来，然后重新灌入 mq 里面去，把白天丢的数据给他补回来。也只能是这样了。假设 1 万个订单积压在 mq 里面，没有处理，其中 1000 个订单都丢了，你只能手动写程序把那 1000 个订单给查出来，手动发到 mq 里去再补一次。

**mq消息队列块满了：**

如果消息积压在 mq 里，你很长时间都没有处理掉，此时导致 mq 都快写满了，咋办？这个还有别的办法吗？没有，谁让你第一个方案执行的太慢了，你临时写程序，接入数据来消费，消费一个丢弃一个，都不要了，快速消费掉所有的消息。然后走第二个方案，到了晚上再补数据吧。


### [2、为什么说保证 message 被可靠持久化的条件是 queue 和 exchange 具有durable 属性，同时 message 具有 persistent 属性才行？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#2为什么说保证-message-被可靠持久化的条件是-queue-和-exchange-具有durable-属性同时-message-具有-persistent-属性才行)  


binding 关系可以表示为 exchange – binding – queue 。从文档中我们知道，若要求投递的 message 能够不丢失，要求 message 本身设置 persistent 属性，要求 exchange和 queue 都设置 durable 属性。

其实这问题可以这么想，若 exchange 或 queue 未设置durable 属性，则在其 crash 之后就会无法恢复，那么即使 message 设置了 persistent 属性，仍然存在 message 虽然能恢复但却无处容身的问题；同理，若 message 本身未设置persistent 属性，则 message 的持久化更无从谈起。


### [3、如何自动删除长时间没有消费的消息？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#3如何自动删除长时间没有消费的消息)  


```
// 通过队列属性设置消息过期时间
Map<String, Object> argss = new HashMap<String, Object>();
argss.put("x-message-ttl",6000);

// 对每条消息设置过期时间
AMQP.BasicProperties properties = new AMQP.BasicProperties.Builder()
    .expiration("10000") // TTL
```


### [4、RabbitMQ 概念里的 channel、exchange 和 queue 这些东东是逻辑概念，还是对应着进程实体？这些东东分别起什么作用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#4rabbitmq-概念里的-channelexchange-和-queue-这些东东是逻辑概念还是对应着进程实体这些东东分别起什么作用)  


queue 具有自己的 erlang 进程；exchange 内部实现为保存 binding 关系的查找表；channel 是实际进行路由工作的实体，即负责按照 routing_key 将 message 投递给queue 。由 AMQP 协议描述可知，channel 是真实 TCP 连接之上的虚拟连接，所有AMQP 命令都是通过 channel 发送的，且每一个 channel 有唯一的 ID。

一个 channel 只能被单独一个操作系统线程使用，故投递到特定 channel 上的 message 是有顺序的。但一个操作系统线程上允许使用多个 channel 。channel 号为 0 的 channel 用于处理所有对于当前 connection 全局有效的帧，而 1-65535 号 channel 用于处理和特定 channel 相关的帧。AMQP 协议给出的 channel ，其中每一个 channel 运行在一个独立的线程上，多线程共享同一个 socket。


### [5、消费者获取消息的方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#5消费者获取消息的方式)  


推

拉


### [6、使用RabbitMQ有什么好处？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#6使用rabbitmq有什么好处)  


**1、** 解耦，系统A在代码中直接调用系统B和系统C的代码，如果将来D系统接入，系统A还需要修改代码，过于麻烦！

**2、** 异步，将消息写入消息队列，非必要的业务逻辑以异步的方式运行，加快响应速度

**3、** 削峰，并发量大的时候，所有的请求直接怼到数据库，造成数据库连接异常


### [7、mq的缺点](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#7mq的缺点)  


**系统可用性降低**

系统引入的外部依赖越多，越容易挂掉，本来你就是A系统调用BCD三个系统的接口就好了，人ABCD四个系统好好的，没啥问题，你偏加个MQ进来，万一MQ挂了咋整？MQ挂了，整套系统崩溃了，你不就完了么。

**系统复杂性提高**

硬生生加个MQ进来，你怎么保证消息没有重复消费？怎么处理消息丢失的情况？怎么保证消息传递的顺序性？头大头大，问题一大堆，痛苦不已

**一致性问题**

**1、** A系统处理完了直接返回成功了，人都以为你这个请求就成功了；但是问题是，要是BCD三个系统那里，BD两个系统写库成功了，结果C系统写库失败了，咋整？你这数据就不一致了。

**2、** 所以消息队列实际是一种非常复杂的架构，你引入它有很多好处，但是也得针对它带来的坏处做各种额外的技术方案和架构来规避掉，最好之后，你会发现，妈呀，系统复杂度提升了一个数量级，也许是复杂了10倍。但是关键时刻，用，还是得用的


### [8、死信队列？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#8死信队列)  


DLX，全称为 Dead-Letter-Exchange，死信交换器，死信邮箱。当消息在一个队列中变成死信 (dead message) 之后，它能被重新被发送到另一个交换器中，这个交换器就是 DLX，绑定 DLX 的队列就称之为死信队列。


### [9、Binding绑定？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#9binding绑定)  


通过绑定将交换器和队列关联起来，一般会指定一个BindingKey,这样RabbitMq就知道如何正确路由消息到队列了。


### [10、消息传输保证层级？](https://gitee.com/souyunku/DevBooks/blob/master/docs/RabbitMQ/RabbitMQ最新2021年面试题大汇总，附答案.md#10消息传输保证层级)  


At most once:最多一次。消息可能会丢失，单不会重复传输。

At least once：最少一次。消息觉不会丢失，但可能会重复传输。

Exactly once: 恰好一次，每条消息肯定仅传输一次。


### 11、如何保证消息的可靠性投递?
### 12、如何保证消息不被重复消费？或者说，如何保证消息消费时的幂等性？
### 13、如何防止出现 blackholed 问题？
### 14、RabbitMQ 允许发送的 message 最大可达多大？
### 15、如何保证消息的顺序性?
### 16、使用RabbitMQ有什么好处？
### 17、RabbitMQ 什么是信道？
### 18、如何确保消息不丢失？
### 19、如何保证RabbitMQ消息的可靠传输？
### 20、什么是RoutingKey路由键？
### 21、延迟队列？
### 22、如何确保消息正确地发送至 RabbitMQ？ 如何确保消息接收方消费了消息？
### 23、如何保证RabbitMQ消息的可靠传输？
### 24、AMQP是什么?
### 25、消息怎么路由？
### 26、Kafka、ActiveMQ、RabbitMQ、RocketMQ 有什么优缺点？
### 27、什么是rabbitmq





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




