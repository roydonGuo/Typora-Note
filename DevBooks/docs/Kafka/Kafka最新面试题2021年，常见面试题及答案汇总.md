# Kafka最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、3.它还可以在记录进入时对其进行处理。Apache Kafka对于新手的面试](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#13它还可以在记录进入时对其进行处理。apache-kafka对于新手的面试)  

### [2、Broker的Heap Size如何设置？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#2broker的heap-size如何设置)  


**1、** 其实对于SRE还是送分题，因为目前来讲大部分公司的业务系统都是使用Java开发，因此SRE对于基本的JVM相关的参数应该至少都是非常了解的，核心就在于JVM的配置以及GC相关的知识。

**2、** 标准答案：任何Java进程JVM堆大小的设置都需要仔细地进行考量和测试。一个常见的做法是，以默认的初始JVM堆大小运行程序，当系统达到稳定状态后，手动触发一次Full GC，然后通过JVM工具查看GC后的存活对象大小。之后，将堆大小设置成存活对象总大小的1.5~2倍。对于Kafka而言，这个方法也是适用的。不过，业界有个最佳实践，那就是将Broker的Heap Size固定为6GB。经过很多公司的验证，这个大小是足够且良好的。


### [3、Rebalance有什么影响](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#3rebalance有什么影响)  


Rebalance本身是Kafka集群的一个保护设定，用于剔除掉无法消费或者过慢的消费者，然后由于我们的数据量较大，同时后续消费后的数据写入需要走网络IO，很有可能存在依赖的第三方服务存在慢的情况而导致我们超时。Rebalance对我们数据的影响主要有以下几点：

数据重复消费: 消费过的数据由于提交offset任务也会失败，在partition被分配给其他消费者的时候，会造成重复消费，数据重复且增加集群压力

Rebalance扩散到整个ConsumerGroup的所有消费者，因为一个消费者的退出，导致整个Group进行了Rebalance，并在一个比较慢的时间内达到稳定状态，影响面较大

频繁的Rebalance反而降低了消息的消费速度，大部分时间都在重复消费和Rebalance

数据不能及时消费，会累积lag，在Kafka的TTL之后会丢弃数据 上面的影响对于我们系统来说，都是致命的。


### [4、Kafka的高可用机制是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#4kafka的高可用机制是什么)  


这个问题比较系统，回答出Kafka的系统特点，leader和follower的关系，消息读写的顺序即可。

[https://www.cnblogs.com/qingyunzong/p/9004703.html](https://www.cnblogs.com/qingyunzong/p/9004703.html)

[https://www.tuicool.com/articles/BNRza2E](https://www.tuicool.com/articles/BNRza2E)

[https://yq.aliyun.com/articles/64703](https://yq.aliyun.com/articles/64703)


### [5、解释Kafka可以接收的消息最大为多少？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#5解释kafka可以接收的消息最大为多少)  


Kafka可以接收的最大消息大小约为1000000字节。


### [6、Kafka流的特点。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#6kafka流的特点。)  


Kafka流的一些最佳功能是Kafka Streams具有高度可扩展性和容错性。Kafka部署到容器，VM，裸机，云。我们可以说，Kafka流对于小型，中型和大型用例同样可行。此外，它完全与Kafka安全集成。编写标准Java应用程序。完全一次处理语义。而且，不需要单独的处理集群。


### [7、Kafka Follower如何与Leader同步数据?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#7kafka-follower如何与leader同步数据)  


Kafka 的复制机制既不是完全的同步复制，也不是单纯的异步复制。完全同步复制要求 All Alive Follower 都复制完，这条消息才会被认为 commit，这种复制方式极大的影响了吞吐率。而异步复制方式下，Follower 异步的从 Leader 复制数据，数据只要被 Leader 写入 log 就被认为已经 commit，这种情况下，如果 leader 挂掉，会丢失数据，Kafka 使用 ISR 的方式很好的均衡了确保数据不丢失以及吞吐率。Follower 可以批量的从 Leader 复制数据，而且 Leader 充分利用磁盘顺序读以及 send file(zero copy) 机制，这样极大的提高复制性能，内部批量写磁盘，大幅减少了 Follower 与 Leader 的消息量差。


### [8、Kafka的哪些场景中使用了零拷贝（Zero Copy）？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#8kafka的哪些场景中使用了零拷贝zero-copy)  


**1、** 其实这道题对于SRE来讲，有点超纲了，不过既然Zero Copy是Kafka高性能的保证，我们需要了解它。

**2、** Zero Copy是特别容易被问到的高阶题目。在Kafka中，体现Zero Copy使用场景的地方有两处：基于mmap的索引和日志文件读写所用的TransportLayer。

**3、** 先说第一个。索引都是基于MappedByteBuffer的，也就是让用户态和内核态共享内核态的数据缓冲区，此时，数据不需要复制到用户态空间。不过，mmap虽然避免了不必要的拷贝，但不一定就能保证很高的性能。在不同的操作系统下，mmap的创建和销毁成本可能是不一样的。很高的创建和销毁开销会抵消Zero Copy带来的性能优势。由于这种不确定性，在Kafka中，只有索引应用了mmap，最核心的日志并未使用mmap机制。

**4、** 再说第二个。TransportLayer是Kafka传输层的接口。它的某个实现类使用了FileChannel的transferTo方法。该方法底层使用sendfile实现了Zero Copy。对Kafka而言，如果I/O通道使用普通的PLAINTEXT，那么，Kafka就可以利用Zero Copy特性，直接将页缓存中的数据发送到网卡的Buffer中，避免中间的多次拷贝。相反，如果I/O通道启用了SSL，那么，Kafka便无法利用Zero Copy特性了。


### [9、副本长时间不在ISR中，这意味着什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#9副本长时间不在isr中这意味着什么)  


意味着 follower 不能像 leader 收集数据那样快速地获取数据。


### [10、：46, 48](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新面试题2021年，常见面试题及答案汇总.md#10：46,-48)  


### 11、Kafka中的数据日志是什么？
### 12、Kafka为何这么快
### 13、Kafka 创建 Topic 时如何将分区放置到不同的 Broker 中
### 14、消费者故障，出现活锁问题如何解决？
### 15、什么是Apache Kafka?
### 16、传统的消息传递方法有哪些类型？
### 17、consumer_offsets是做什么用的？
### 18、解释Kafka Producer API的作用。
### 19、阐述下 Kafka 中的领导者副本（Leader Replica）和追随者副本（Follower Replica）的区别
### 20、讲讲Kafka维护消费状态跟踪的方法
### 21、Kafka 的消费者如何消费数据
### 22、为什么Kafka的复制至关重要？
### 23、如何保证Kafka顺序消费
### 24、Apache Kafka是分布式流处理平台吗？如果是，你能用它做什么？
### 25、为什么Kafka的复制至关重要？
### 26、消费者如何不自动提交偏移量，由应用提交？
### 27、Kafka 新建的分区会在哪个目录下创建
### 28、Kafka中的 zookeeper 起到什么作用？可以不用zookeeper吗？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




