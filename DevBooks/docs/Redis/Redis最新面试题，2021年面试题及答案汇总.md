# Redis最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、为什么 edis 需要把所有数据放到内存中？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#1为什么-edis-需要把所有数据放到内存中)  


Redis 为了达到最快的读写速度将数据都读到内存中，并通过异步的方式将数据写入磁盘。所以 Redis 具有快速和数据持久化的特征。如果不将数据放在内存中， 磁盘 I/O 速度为严重影响 Redis 的性能。在内存越来越便宜的今天， Redis 将会越来越受欢迎。如果设置了最大使用的内存， 则数据已有记录数达到内存限值后不能继续插入新值。


### [2、MySQL里有2000w数据，Redis中只存20w的数据](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#2mysql里有2000w数据redis中只存20w的数据)  


**如何保证Redis中的数据都是热点数据？**

Redis内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。

其实面试除了考察Redis，不少公司都很重视高并发高可用的技术，特别是一线互联网公司，分布式、JVM、spring源码分析、微服务等知识点已是面试的必考题。我自己整理收集了一套系统的架构技术体系，针对当前互联网公司的技术需求以及结合主流技术，这些东西可能你们平时在工作中接触过，但是缺少的全面系统的学习，加入
### [3、Reids6种淘汰策略：](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#3reids6种淘汰策略：)  


**noeviction**: 不删除策略, 达到最大内存限制时, 如果需要更多内存, 直接返回错误信息。大多数写命令都会导致占用更多的内存(有极少数会例外。

**allkeys-lru:**所有key通用; 优先删除最近最少使用(less recently used ,LRU) 的 key。

**volatile-lru:**只限于设置了 expire 的部分; 优先删除最近最少使用(less recently used ,LRU) 的 key。

**allkeys-random:**所有key通用; 随机删除一部分 key。

**volatile-random**: 只限于设置了 **expire** 的部分; 随机删除一部分 key。

**volatile-ttl**: 只限于设置了 **expire** 的部分; 优先删除剩余时间(time to live,TTL) 短的key。


### [4、Redis还提供的高级工具](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#4redis还提供的高级工具)  


像慢查询分析、性能测试、Pipeline、事务、Lua自定义命令、Bitmaps、HyperLogLog、/订阅、Geo等个性化功能。


### [5、Pipeline 有什么好处，为什么要用pipeline？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#5pipeline-有什么好处为什么要用pipeline)  


可以将多次 IO 往返的时间缩减为一次，前提是 pipeline 执行的指令之间没有因果相关性。使用 Redis-benchmark 进行压测的时候可以发现影响 Redis 的 QPS 峰值的一个重要因素是 pipeline 批次指令的数目。


### [6、Redis 集群方案什么情况下会导致整个集群不可用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#6redis-集群方案什么情况下会导致整个集群不可用)  


有 A， B， C 三个节点的集群,在没有复制模型的情况下,如果节点 B 失败了， 那么整个集群就会以为缺少 5501-11000 这个范围的槽而不可用。


### [7、Redis 的内存用完了会发生什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#7redis-的内存用完了会发生什么)  


如果达到设置的上限，Redis 的写命令会返回错误信息（ 但是读命令还可以正常返回。） 或者你可以将 Redis 当缓存来使用配置淘汰机制， 当 Redis 达到内存上限时会冲刷掉旧的内容。


### [8、删除key](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#8删除key)  


```
del key1 key2 ...
```


### [9、Redis集群最大节点个数是多少？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#9redis集群最大节点个数是多少)  


16384个。


### [10、Redis 到底是怎么实现“附近的人”](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题，2021年面试题及答案汇总.md#10redis-到底是怎么实现“附近的人)  


```
GEOADD key longitude latitude member [longitude latitude member ...]
```

将给定的位置对象（纬度、经度、名字）添加到指定的key。其中，key为集合名称，member为该经纬度所对应的对象。在实际运用中，当所需存储的对象数量过多时，可通过设置多key(如一个省一个key)的方式对对象集合变相做sharding，避免单集合数量过多。

**成功插入后的返回值：**

```
(integer) N
```

其中N为成功插入的个数。



### 11、什么是Redis?
### 12、Redis集群方案应该怎么做？都有哪些方案？
### 13、Redis官方为什么不提供Windows版本？
### 14、Redis的并发竞争问题如何解决?
### 15、Memcache 与Redis 的区别都有哪些？
### 16、Redis 是单进程单线程的？
### 17、Redis是单线程的，但Redis为什么这么快？
### 18、Redis 回收进程如何工作的?
### 19、支持一致性哈希的客户端有哪些？
### 20、一个字符串类型的值能存储最大容量是多少？
### 21、Redis回收进程如何工作的？
### 22、假如 Redis 里面有 1 亿个key，其中有 10w 个key 是以某个固定的已知的前缀开头的，如果将它们全部找出来？
### 23、Redis常见性能问题和解决方案：
### 24、Redis 集群最大节点个数是多少？
### 25、Redis 的主从复制
### 26、Reids工具命令
### 27、多节点 Redis 分布式锁：Redlock 算法
### 28、Redis常见性能问题和解决方案？
### 29、Redis 的同步机制了解么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




