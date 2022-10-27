# Kafka最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、在生产者中，何时发生QueueFullException？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#1在生产者中何时发生queuefullexception)  


每当Kafka生产者试图以代理的身份在当时无法处理的速度发送消息时，通常都会发生QueueFullException。但是，为了协作处理增加的负载，用户需要添加足够的代理，因为生产者不会阻止。


### [2、如何估算Kafka集群的机器数量？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#2如何估算kafka集群的机器数量)  


**1、** 该题也算是SRE的送分题吧，对于SRE来讲，任何生产的系统第一步需要做的就是容量预估以及集群的架构规划，实际上也就是机器数量和所用资源之间的关联关系，资源通常来讲就是CPU，内存，磁盘容量，带宽。但需要注意的是，Kafka因为独有的设计，对于磁盘的要求并不是特别高，普通机械硬盘足够，而通常的瓶颈会出现在带宽上。

**2、** 在预估磁盘的占用时，你一定不要忘记计算副本同步的开销。如果一条消息占用1KB的磁盘空间，那么，在有3个副本的主题中，你就需要3KB的总空间来保存这条消息。同时，需要考虑到整个业务Topic数据保存的最大时间，以上几个因素，基本可以预估出来磁盘的容量需求。

**3、** 需要注意的是：对于磁盘来讲，一定要提前和业务沟通好场景，而不是等待真正有磁盘容量瓶颈了才去扩容磁盘或者找业务方沟通方案。

**4、** 对于带宽来说，常见的带宽有1Gbps和10Gbps，通常我们需要知道，当带宽占用接近总带宽的90%时，丢包情形就会发生。


### [3、分区Leader选举策略有几种？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#3分区leader选举策略有几种)  


分区的Leader副本选举对用户是完全透明的，它是由Controller独立完成的。你需要回答的是，在哪些场景下，需要执行分区Leader选举。每一种场景对应于一种选举策略。

**1、** OfflinePartition Leader选举：每当有分区上线时，就需要执行Leader选举。所谓的分区上线，可能是创建了新分区，也可能是之前的下线分区重新上线。这是最常见的分区Leader选举场景。

**2、** ReassignPartition Leader选举：当你手动运行Kafka-reassign-partitions命令，或者是调用Admin的alterPartitionReassignments方法执行分区副本重分配时，可能触发此类选举。假设原来的AR是[1，2，3]，Leader是1，当执行副本重分配后，副本集合AR被设置成[4，5，6]，显然，Leader必须要变更，此时会发生Reassign Partition Leader选举。

**3、** PreferredReplicaPartition Leader选举：当你手动运行Kafka-preferred-replica-election命令，或自动触发了Preferred Leader选举时，该类策略被激活。所谓的Preferred Leader，指的是AR中的第一个副本。比如AR是[3，2，1]，那么，Preferred Leader就是3。

**4、** ControlledShutdownPartition Leader选举：当Broker正常关闭时，该Broker上的所有Leader副本都会下线，因此，需要为受影响的分区执行相应的Leader选举。

这4类选举策略的大致思想是类似的，即从AR中挑选首个在ISR中的副本，作为新Leader。


### [4、Kafka中有哪几个组件?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#4kafka中有哪几个组件)  


Kafka最重要的元素是：

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/1/27/0/9_1.png#alt=9%5C_1.png)

主题：Kafka主题是一堆或一组消息。生产者：在Kafka，生产者发布通信以及向Kafka主题发布消息。消费者：Kafka消费者订阅了一个主题，并且还从主题中读取和处理消息。经纪人：在管理主题中的消息存储时，我们使用Kafka Brokers。


### [5、：24, 22](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#5：24,-22)  



### [6、系统工具有哪些类型？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#6系统工具有哪些类型)  


系统工具有三种类型：1.Kafka迁移工具：它有助于将代理从一个版本迁移到另一个版本。2.Mirror Maker：Mirror Maker工具有助于将一个Kafka集群的镜像提供给另一个。3.消费者检查:对于指定的主题集和消费者组，它显示主题，分区，所有者。


### [7、比较传统队列系统与Apache Kafka](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#7比较传统队列系统与apache-kafka)  


让我们比较一下传统队列系统与Apache Kafka的功能：消息保留 传统的队列系统 - 它通常从队列末尾处理完成后删除消息。 Apache Kafka中，消息即使在处理后仍然存在。这意味着Kafka中的消息不会因消费者收到消息而被删除。基于逻辑的处理传统队列系统不允许基于类似消息或事件处理逻辑。Apache Kafka允许基于类似消息或事件处理逻辑。


### [8、连接器API的作用是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#8连接器api的作用是什么)  


一个允许运行和构建可重用的生产者或消费者的API，将Kafka主题连接到现有的应用程序或数据系统，我们称之为连接器API。Apache Kafka对于新手的面试
### [9、消息队列的作用](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#9消息队列的作用)  


**解耦**

快递小哥手上有很多快递需要送，他每次都需要先电话一一确认收货人是否有空、哪个时间段有空，然后再确定好送货的方案。这样完全依赖收货人了！如果快递一多，快递小哥估计的忙疯了……

如果有了便利店，快递小哥只需要将同一个小区的快递放在同一个便利店，然后通知收货人来取货就可以了，这时候快递小哥和收货人就实现了解耦！

**异步**

快递小哥打电话给我后需要一直在你楼下等着，直到我拿走你的快递他才能去送其他人的。快递小哥将快递放在小芳便利店后，又可以干其他的活儿去了，不需要等待你到来而一直处于等待状态。提高了工作的效率。

**削峰**

假设双十一我买了不同店里的各种商品，而恰巧这些店发货的快递都不一样，有中通、圆通、申通、各种通等……

更巧的是他们都同时到货了！中通的小哥打来电话叫我去北门取快递、圆通小哥叫我去南门、申通小哥叫我去东门。我一时手忙脚乱……

我们能看到在系统需要交互的场景中，使用消息队列中间件真的是好处多多，基于这种思路，就有了丰巢、菜鸟驿站等比小芳便利店更专业的“中间件”了。


### [10、数据传输的事物定义有哪三种？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题，高级面试题及附答案解析.md#10数据传输的事物定义有哪三种)  


**数据传输的事务定义通常有以下三种级别：**

**1、** 最多一次: 消息不会被重复发送，最多被传输一次，但也有可能一次不传输

**2、** 最少一次: 消息不会被漏发送，最少被传输一次，但也有可能被重复传输、（3）精确的一次（Exactly once）: 不会漏传输也不会重复传输,每个消息都传输被一次而

**3、** 且仅仅被传输一次，这是大家所期望的


### 11、Kafka 存储在硬盘上的消息格式是什么？
### 12、在Kafka中，ZooKeeper的作用是什么？
### 13、Kafka能手动删除消息吗？
### 14、什么是复制工具及其类型？
### 15、什么是Kafka？
### 16、消费者提交消费位移时提交的是当前消费到的最新消息的offset还是offset+1?
### 17、Java Consumer为什么采用单线程来获取消息？
### 18、Kafka 中的消息是否会丢失和重复消费？
### 19、LEO、LSO、AR、ISR、HW都表示什么含义？
### 20、能说一下leader选举过程吗
### 21、解释多租户是什么？
### 22、Kafka一次reblance大概要多久
### 23、：12,15,20
### 24、什么情况下一个 Broker 会从ISR中踢出去?
### 25、启动Kafka服务器的过程是什么？
### 26、解释下Kafka中位移（offset）的作用
### 27、说明Kafka的一个最佳特征。
### 28、消费者负载均衡策略





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




