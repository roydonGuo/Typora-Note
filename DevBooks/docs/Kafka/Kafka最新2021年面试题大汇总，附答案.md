# Kafka最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、解释生产者是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#1解释生产者是什么)  


生产者的主要作用是将数据发布到他们选择的主题上。基本上，它的职责是选择要分配给主题内分区的记录。


### [2、什么是多租户？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#2什么是多租户)  


我们可以轻松地将Kafka部署为多租户解决方案。但是，通过配置主题可以生成或使用数据，可以启用多租户。此外，它还为配额提供操作支持。


### [3、Kafka为什么不支持读写分离？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#3kafka为什么不支持读写分离)  


**1、** 这其实是分布式场景下的通用问题，因为我们知道CAP理论下，我们只能保证C（一致性）和A（可用性）取其一，如果支持读写分离，那其实对于一致性的要求可能就会有一定折扣，因为通常的场景下，副本之间都是通过同步来实现副本数据一致的，那同步过程中肯定会有时间的消耗，如果支持了读写分离，就意味着可能的数据不一致，或数据滞后。

**2、** Leader/Follower模型并没有规定Follower副本不可以对外提供读服务。很多框架都是允许这么做的，只是 Kafka最初为了避免不一致性的问题，而采用了让Leader统一提供服务的方式。

**3、** 不过，自Kafka 2.4之后，Kafka提供了有限度的读写分离，也就是说，Follower副本能够对外提供读服务。


### [4、：35, 36, 37](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#4：35,-36,-37)  



### [5、：11,13,14,16,17,18,19Apache Kafka对于有经验的人的面试](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#5：11,13,14,16,17,18,19apache-kafka对于有经验的人的面试)  

### [6、Leader和Follower的概念是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#6leader和follower的概念是什么)  


在Kafka的每个分区中，都有一个服务器充当leader，0到多个服务器充当follower的角色。


### [7、Kafka和Flume之间的主要区别是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#7kafka和flume之间的主要区别是什么)  


**工具类型**

Apache Kafka 是面向多个生产商和消费者的通用工具。

Apache Flume 是特定应用程序的专用工具。

**复制功能**

Apache Kafka 可以复制事件；

Apache Flume 不复制事件。


### [8、没有ZooKeeper可以使用Kafka吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#8没有zookeeper可以使用kafka吗)  


绕过Zookeeper并直接连接到Kafka服务器是不可能的，所以答案是否定的。如果以某种方式，使ZooKeeper关闭，则无法为任何客户端请求提供服务。


### [9、为什么需要消息系统，MySQL不能满足需求吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#9为什么需要消息系统mysql不能满足需求吗)  


**1、** 解耦：

允许你独立的扩展或修改两边的处理过程，只要确保它们遵守同样的接口约束。

**2、** 冗余：

消息队列把数据进行持久化直到它们已经被完全处理，通过这一方式规避了数据丢失风险。许多消息队列所采用的”插入-获取-删除”范式中，在把一个消息从队列中删除之前，需要你的处理系统明确的指出该消息已经被处理完毕，从而确保你的数据被安全的保存直到你使用完毕。

**3、** 扩展性：

因为消息队列解耦了你的处理过程，所以增大消息入队和处理的频率是很容易的，只要另外增加处理过程即可。

**4、** 灵活性 & 峰值处理能力：

在访问量剧增的情况下，应用仍然需要继续发挥作用，但是这样的突发流量并不常见。如果为以能处理这类峰值访问为标准来投入资源随时待命无疑是巨大的浪费。使用消息队列能够使关键组件顶住突发的访问压力，而不会因为突发的超负荷的请求而完全崩溃。

**5、** 可恢复性：

系统的一部分组件失效时，不会影响到整个系统。消息队列降低了进程间的耦合度，所以即使一个处理消息的进程挂掉，加入队列中的消息仍然可以在系统恢复后被处理。

**6、** 顺序保证：

在大多使用场景下，数据处理的顺序都很重要。大部分消息队列本来就是排序的，并且能保证数据会按照特定的顺序来处理。（Kafka 保证一个 Partition 内的消息的有序性）

**7、** 缓冲：

有助于控制和优化数据流经过系统的速度，解决生产消息和消费消息的处理速度不一致的情况。

**8、** 异步通信：

很多时候，用户不想也不需要立即处理消息。消息队列提供了异步处理机制，允许用户把一个消息放入队列，但并不立即处理它。想向队列中放入多少消息就放多少，然后在需要的时候再去处理它们。


### [10、为什么要使用 Kafka？为什么要使用消息队列？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题大汇总，附答案.md#10为什么要使用-kafka为什么要使用消息队列)  


1. 缓冲和削峰：上游数据时有突发流量，下游可能扛不住，或者下游没有足够多的机器来保证冗余，Kafka在中间可以起到一个缓冲的作用，把消息暂存在Kafka中，下游服务就可以按照自己的节奏进行慢慢处理。
2. 解耦和扩展性：项目开始的时候，并不能确定具体需求。消息队列可以作为一个接口层，解耦重要的业务流程。只需要遵守约定，针对数据编程即可获取扩展能力。
3. 冗余：可以采用一对多的方式，一个生产者消息，可以被多个订阅topic的服务消费到，供多个毫无关联的业务使用。
4. 健壮性：消息队列可以堆积请求，所以消费端业务即使短时间死掉，也不会影响主要业务的正常进行。
5. 异步通信：很多时候，用户不想也不需要立即处理消息。消息队列提供了异步处理机制，允许用户把一个消息放入队列，但并不立即处理它。想向队列中放入多少消息就放多少，然后在需要的时候再去处理它们。


### 11、没有zookeeper可以使用Kafka吗？
### 12、Kafka 与传统MQ消息系统之间有三个关键区别
### 13、解释偏移的作用。
### 14、解释术语“Log Anatomy”
### 15、副本和ISR扮演什么角色？
### 16、比较RabbitMQ与Apache Kafka
### 17、Apache Kafka是什么？
### 18、consumer是推还是拉？
### 19、如果副本长时间不在ISR中，这意味着什么？
### 20、数据有序
### 21、怎么解决rebalance中遇到的问题呢？
### 22、Kafka分布式（不是单机）的情况下，如何保证消息的顺序消费?
### 23、能简单说一下rebalance过程吗？
### 24、讲一讲Kafka的ack的三种机制
### 25、Apache Kafka是分布式流处理平台吗？如果是，你能用它做什么？
### 26、什么是Kafka中的地域复制？
### 27、在Kafka集群中保留期的目的是什么？
### 28、Kafka的message格式是什么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




