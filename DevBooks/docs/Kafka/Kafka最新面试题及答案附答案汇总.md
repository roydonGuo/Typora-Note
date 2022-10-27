# Kafka最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Kafka Producer如何优化写入速度?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#1kafka-producer如何优化写入速度)  


1. 增加线程
2. 提高 batch.size
3. 增加更多 producer 实例
4. 增加 partition 数
5. 设置 acks=-1 时，如果延迟增大：可以增大 num.replica.fetchers（follower 同步数据的线程数）来调解；
6. 跨数据中心的传输：增加 socket 缓冲区设置以及 OS tcp 缓冲区设置。


### [2、生产者中，什么情况下会发生 QueueFullException？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#2生产者中什么情况下会发生-queuefullexception)  


每当Kafka生产者试图以代理的身份在当时无法处理的速度发送消息时，通常都会发生QueueFullException。但是，为了协作处理增加的负载，用户需要添加足够的代理，因为生产者不会阻止。


### [3、数据传输的事务定义有哪三种？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#3数据传输的事务定义有哪三种)  


**和MQTT的事务定义一样都是3种**

**1、** 最多一次: 消息不会被重复发送，最多被传输一次，但也有可能一次不传输

**2、** 最少一次: 消息不会被漏发送，最少被传输一次，但也有可能被重复传输.

**3、** 精确的一次（Exactly once）: 不会漏传输也不会重复传输,每个消息都传输被一次而且仅仅被传输一次，这是大家所期望的


### [4、Kafka Unclean 配置代表什么？会对 spark streaming 消费有什么影响？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#4kafka-unclean-配置代表什么会对-spark-streaming-消费有什么影响)  


unclean.leader.election.enable 为 true 的话，意味着非 ISR 集合的 broker 也可以参与选举，这样有可能就会丢数据，spark streaming在消费过程中拿到的 end offset 会突然变小，导致 spark streaming job 挂掉。如果 unclean.leader.election.enable 参数设置为 true，就有可能发生数据丢失和数据不一致的情况，Kafka 的可靠性就会降低；而如果 unclean.leader.election.enable 参数设置为 false，Kafka 的可用性就会降低。


### [5、Kafka 中 Consumer Group 是什么概念？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#5kafka-中-consumer-group-是什么概念)  


同样是逻辑上的概念，是Kafka实现单播和广播两种消息模型的手段。同一个topic的数据，会广播给不同的group；同一个group中的worker，只有一个worker能拿到这个数据。换句话说，对于同一个topic，每个group都可以拿到同样的所有数据，但是数据进入group后只能被其中的一个worker消费。group内的worker可以使用多线程或多进程来实现，也可以将进程分散在多台机器上，worker的数量通常不超过partition的数量，且二者最好保持整数倍关系，因为Kafka在设计时假定了一个partition只能被一个worker消费（同一group内）。


### [6、什么是生产者？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#6什么是生产者)  


生产者的主要作用是将数据到他们选择的主题上。基本上，它的职责是选择要分配给主题内分区的记录。


### [7、Kafka 与传统消息系统之间有三个关键区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#7kafka-与传统消息系统之间有三个关键区别)  


**1、** Kafka 持久化日志，这些日志可以被重复读取和无限期保留

**2、** Kafka 是一个分布式系统：它以集群的方式运行，可以灵活伸缩，在内部通过复制数据

**3、** 提升容错能力和高可用性

**4、** Kafka 支持实时的流式处理


### [8、Kafka 中是怎么体现消息顺序性的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#8kafka-中是怎么体现消息顺序性的)  


Kafka 每个 partition 中的消息在写入时都是有序的，消费时，每个 partition 只能被每一个 group 中的一个消费者消费，保证了消费时也是有序的。整个 topic 不保证有序。如果为了保证 topic 整个有序，那么将 partition 调整为1.


### [9、Apache Kafka的缺陷](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#9apache-kafka的缺陷)  


Kafka的局限性是：1.没有完整的监控工具集2.消息调整的
### [10、解释Apache Kafka用例？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题及答案附答案汇总.md#10解释apache-kafka用例)  


Apache Kafka有很多用例，例如：

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/1/27/0/9_4.png#alt=9%5C_4.png)

Kafka指标可以使用Kafka进行操作监测数据。此外，为了生成操作数据的集中提要，它涉及到从分布式应用程序聚合统计信息。Kafka日志聚合 从组织中的多个服务收集日志。流处理在流处理过程中，Kafka的强耐久性非常有用。Apache Kafka对于新手的面试
### 11、什么是消费者或用户？
### 12、Controller发生网络分区（Network Partitioning）时，Kafka会怎么样？
### 13、当ack为-1时，什么情况下，Leader 认为一条消息 Commit了？
### 14、Kafka判断一个节点是否还活着有那两个条件？
### 15、偏移的作用是什么？
### 16、Kafka 如何判断节点是否存活
### 17、ISR在Kafka环境中代表什么？
### 18、Java在Apache Kafka中的重要性是什么？
### 19、Kafka中的 Broker 是干什么的？
### 20、连接器API的作用是什么？
### 21、Kafka可以接收的消息最大为多少？
### 22、：41, 42, 43, 44, 45, 47, 49Apache Kafka对于有经验的人的面试
### 23、Kafka中有哪几个组件?
### 24、Kafka 高效文件存储设计特点：
### 25、如何设置Kafka能接收的最大消息的大小？
### 26、3.不支持通配符主题选择4.速度###
### 27、Kafka 判断一个节点是否还活着有那两个条件？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




