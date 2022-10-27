# Kafka最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、是什么确保了Kafka中服务器的负载平衡？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#1是什么确保了kafka中服务器的负载平衡)  


由于领导者的主要角色是执行分区的所有读写请求的任务，而追随者被动地复制领导者。因此，在领导者失败时，其中一个追随者接管了领导者的角色。基本上，整个过程可确保服务器的负载平衡。


### [2、消费者API的作用是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#2消费者api的作用是什么)  


允许应用程序订阅一个或多个主题并处理生成给它们的记录流的API，我们称之为消费者API。


### [3、解释流API的作用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#3解释流api的作用)  


一种允许应用程序充当流处理器的API，它还使用一个或多个主题的输入流，并生成一个输出流到一个或多个输出主题，此外，有效地将输入流转换为输出流，我们称之为流API。


### [4、Kafka为什么那么快?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#4kafka为什么那么快)  


1. Cache Filesystem Cache PageCache缓存
2. 顺序写 由于现代的操作系统提供了预读和写技术，磁盘的顺序写大多数情况下比随机写内存还要快。
3. Zero-copy 零拷技术减少拷贝次数
4. Batching of Messages 批量量处理。合并小的请求，然后以流的方式进行交互，直顶网络上限。
5. Pull 拉模式 使用拉模式进行消息的获取消费，与消费端处理能力相符。


### [5、Kafka系统工具有哪些类型？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#5kafka系统工具有哪些类型)  


**1、** Kafka迁移工具：它有助于将代理从一个版本迁移到另一个版本。

**2、** Mirror Maker：Mirror Maker工具有助于将一个Kafka集群的镜像提供给另一个。

**3、** 消费者检查:对于指定的主题集和消费者组，它显示主题，分区，所有者。


### [6、partition 的数据如何保存到硬盘](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#6partition-的数据如何保存到硬盘)  


topic 中的多个 partition 以文件夹的形式保存到 broker，每个分区序号从 0 递增，

且消息有序

Partition 文件下有多个 segment（xxx.index，xxx.log）

segment 文件里的 大小和配置文件大小一致可以根据要求修改 默认为 1g

如果大小大于 1g 时，会滚动一个新的 segment 并且以上一个 segment 最后一条消息的偏移

量命名


### [7、Zookeeper对于Kafka的作用是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#7zookeeper对于kafka的作用是什么)  


**1、** Zookeeper是一个开放源码的、高性能的协调服务，它用于Kafka的分布式应用。

**2、** Zookeeper主要用于在集群中不同节点之间进行通信

**3、** 在Kafka中，它被用于提交偏移量，因此如果节点在任何情况下都失败了，它都可以从之前提交的偏移量中获取

**4、** 除此之外，它还执行其他活动，如: leader检测、分布式同步、配置管理、识别新节点何时离开或连接、集群、节点实时状态等等。


### [8、流API的作用是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#8流api的作用是什么)  


一种允许应用程序充当流处理器的API，它还使用一个或多个主题的输入流，并生成一个输出流到一个或多个输出主题，此外，有效地将输入流转换为输出流，我们称之为流API。


### [9、Kafka的流处理是什么意思？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#9kafka的流处理是什么意思)  


连续、实时、并发和以逐记录方式处理数据的类型，我们称之为Kafka流处理。


### [10、Kafka集群中保留期的目的是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Kafka/Kafka最新2021年面试题附答案解析，大汇总.md#10kafka集群中保留期的目的是什么)  


保留期限保留了Kafka群集中的所有已记录。它不会检查它们是否已被消耗。此外，可以通过使用保留期的配置设置来丢弃记录。而且，它可以释放一些空间。


### 11、Kafka 的 ack 机制
### 12、：31, 32, 33, 34, 38, 39, 40Apache Kafka对于有经验的人的面试
### 13、简述Follower副本消息同步的完整流程
### 14、解释一些Kafka流实时用例。
### 15、副本和 ISR 扮演什么角色？
### 16、简单说一下ack机制
### 17、producer 是否直接将数据发送到 broker 的 leader(主节点)？
### 18、Kafka如何不消费重复数据？比如扣款，我们不能重复的扣。
### 19、Kafka中有哪几个组件?
### 20、列出所有Apache Kafka业务
### 21、：3,5,6
### 22、什么是消费者组？
### 23、：1,2,4,7,8,9,10Apache Kafka对于有经验的人的面试
### 24、解释术语“主题复制因子”。
### 25、Kafka存在那些局限性？
### 26、如何调优Kafka？
### 27、如何控制消费的位置
### 28、Kafka提供的保证是什么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




