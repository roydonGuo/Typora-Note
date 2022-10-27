# Redis最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、一个Redis实例最多能存放多少的keys？List、Set、Sorted Set他们最多能存放多少元素？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#1一个redis实例最多能存放多少的keyslistsetsorted-set他们最多能存放多少元素)  


理论上Redis可以处理多达232的keys，并且在实际中进行了测试，每个实例至少存放了2亿5千万的keys。我们正在测试一些较大的值。任何list、set、和sorted set都可以放232个元素。换句话说，Redis的存储极限是系统中的可用内存值。


### [2、为什么要做Redis分区？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#2为什么要做redis分区)  


分区可以让Redis管理更大的内存，Redis将可以使用所有机器的内存。如果没有分区，你最多只能使用一台机器的内存。分区使Redis的计算能力通过简单地增加计算机得到成倍提升,Redis的网络带宽也会随着计算机和网卡的增加而成倍增长。


### [3、定时删除](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#3定时删除)  


优点：对内存友好，定时删除策略可以保证过期键会尽可能快地被删除，并释放国期间所占用的内存

缺点：对cpu时间不友好，在过期键比较多时，删除任务会占用很大一部分cpu时间，在内存不紧张但cpu时间紧张的情况下，将cpu时间用在删除和当前任务无关的过期键上，影响服务器的响应时间和吞吐量


### [4、怎么理解Redis事务？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#4怎么理解redis事务)  


事务是一个单独的隔离操作：事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。

事务是一个原子操作：事务中的命令要么全部被执行，要么全部都不执行。


### [5、什么是Redis？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#5什么是redis)  


Redis本质上是一个Key-Value类型的内存数据库，很像Memcached，整个数据库统统加载在内存当中进行操作，定期通过异步操作把数据库数据flush到硬盘上进行保存。因为是纯内存操作，Redis的性能非常出色，每秒可以处理超过 10万次读写操作，是已知性能最快的Key-Value DB。

Redis的出色之处不仅仅是性能，Redis最大的魅力是支持保存多种数据结构，此外单个value的最大限制是1GB，不像 Memcached只能保存1MB的数据，因此Redis可以用来实现很多有用的功能，比方说用他的List来做FIFO双向链表，实现一个轻量级的高性 能消息队列服务，用他的Set可以做高性能的tag系统等等。另外Redis也可以对存入的Key-Value设置expire时间，因此也可以被当作一 个功能加强版的Memcached来用。

Redis的主要缺点是数据库容量受到物理内存的限制，不能用作海量数据的高性能读写，因此Redis适合的场景主要局限在较小数据量的高性能操作和运算上。


### [6、Redis分布式锁实现](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#6redis分布式锁实现)  


先拿setnx来争抢锁，抢到之后，再用expire给锁加一个过期时间防止锁忘记了释放。如果在setnx之后执行expire之前进程意外crash或者要重启维护了，那会怎么样？set指令有非常复杂的参数，这个应该是可以同时把setnx和expire合成一条指令来用的！


### [7、Redis做异步队列](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#7redis做异步队列)  


一般使用list结构作为队列，rpush生产消息，lpop消费消息。当lpop没有消息的时候，要适当sleep一会再重试。缺点：在消费者下线的情况下，生产的消息会丢失，得使用专业的消息队列如rabbitmq等。能不能生产一次消费多次呢？使用pub/sub主题订阅者模式，可以实现1:N的消息队列。


### [8、Reids常用5种数据类型](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#8reids常用5种数据类型)  


string，list，set，sorted set，hash


### [9、Redis 事务相关的命令有哪几个？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#9redis-事务相关的命令有哪几个)  


MULTI、EXEC、DISCARD、WATCH


### [10、WATCH命令和基于CAS的乐观锁：](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题附答案解析，大汇总.md#10watch命令和基于cas的乐观锁：)  


在Redis的事务中，WATCH命令可用于提供CAS(check-and-set)功能。假设我们通过WATCH命令在事务执行之前监控了多个Keys，倘若在WATCH之后有任何Key的值发生了变化，EXEC命令执行的事务都将被放弃，同时返回Null multi-bulk应答以通知调用者事务

执行失败。例如，我们再次假设Redis中并未提供incr命令来完成键值的原子性递增，如果要实现该功能，我们只能自行编写相应的代码。其伪码如下：

```
val = GET mykey
val = val + 1
SET mykey $val
```

以上代码只有在单连接的情况下才可以保证执行结果是正确的，因为如果在同一时刻有多个客户端在同时执行该段代码，那么就会出现多线程程序中经常出现的一种错误场景--竞态争用(race condition)。

比如，客户端A和B都在同一时刻读取了mykey的原有值，假设该值为10，此后两个客户端又均将该值加一后set回Redis服务器，这样就会导致mykey的结果为11，而不是我们认为的12。为了解决类似的问题，我们需要借助WATCH命令的帮助，见如下代码：

```
WATCH mykey
val = GET mykey
val = val + 1
MULTI
SET mykey $val
EXEC
```

和此前代码不同的是，新代码在获取mykey的值之前先通过WATCH命令监控了该键，此后又将set命令包围在事务中，这样就可以有效的保证每个连接在执行EXEC之前，如果当前连接获取的mykey的值被其它连接的客户端修改，那么当前连接的EXEC命令将执行失败。这样调用者在判断返回值后就可以获悉val是否被重新设置成功。


### 11、怎么理解 Redis 事务？
### 12、MySQL 里有 2000w 数据，Redis 中只存 20w 的数据，如何保证Redis 中的数据都是热点数据？
### 13、Redis的缓存失效策略和主键失效机制
### 14、布隆过滤器
### 15、判断key是否存在
### 16、Redis与其他key-value存储有什么不同？
### 17、Redis回收进程如何工作的？
### 18、RDB和AOF的优缺点
### 19、Redis是单进程单线程的
### 20、为什么需要持久化？
### 21、Redis 的数据类型？
### 22、Redis提供了哪几种持久化方式？
### 23、Redis内存模型
### 24、Redis缓存被击穿处理机制
### 25、Redis的全称是什么？
### 26、什么是Redis?
### 27、持久化策略选择
### 28、Redis中的管道有什么用？
### 29、Redis的内存占用情况怎么样？
### 30、手写一个 LRU 算法





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




