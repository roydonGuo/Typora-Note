# Redis最新2022年面试题及答案，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、为什么Redis需要把所有数据放到内存中？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#1为什么redis需要把所有数据放到内存中)  


Redis为了达到最快的读写速度将数据都读到内存中，并通过异步的方式将数据写入磁盘。所以Redis具有快速和数据持久化的特征。如果不将数据放在内存中，磁盘I/O速度为严重影响Redis的性能。在内存越来越便宜的今天，Redis将会越来越受欢迎。

如果设置了最大使用的内存，则数据已有记录数达到内存限值后不能继续插入新值。


### [2、查看Redis使用情况及状态信息用什么命令？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#2查看redis使用情况及状态信息用什么命令)  


info

### [4、修改配置不重启Redis会实时生效吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#4修改配置不重启redis会实时生效吗)  


针对运行实例，有许多配置选项可以通过 CONFIG SET 命令进行修改，而无需执行任何形式的重启。 从 Redis 2.2 开始，可以从 AOF 切换到 RDB 的快照持久性或其他方式而不需要重启 Redis。检索 ‘CONFIG GET *’ 命令获取更多信息。

但偶尔重新启动是必须的，如为升级 Redis 程序到新的版本，或者当你需要修改某些目前 CONFIG 命令还不支持的配置参数的时候。


### [5、是否使用过 Redis 集群，集群的原理是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#5是否使用过-redis-集群集群的原理是什么)  


**1、** Redis Sentinal 着眼于高可用， 在 master 宕机时会自动将 slave 提升为master， 继续提供服务。

**2、** Redis Cluster 着眼于扩展性， 在单个 Redis 内存不足时， 使用 Cluster 进行分片存储。


### [6、缓存并发问题](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#6缓存并发问题)  


这里的并发指的是多个Redis的client同时set key引起的并发问题。比较有效的解决方案就是把Redis.set操作放在队列中使其串行化，必须的一个一个执行，具体的代码就不上了，当然加锁也是可以的，至于为什么不用Redis中的事务，留给各位看官自己思考探究。


### [7、使用过Redis分布式锁么，它是什么回事？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#7使用过redis分布式锁么它是什么回事)  


先拿setnx来争抢锁，抢到之后，再用expire给锁加一个过期时间防止锁忘记了释放。

这时候对方会告诉你说你回答得不错，然后接着问如果在setnx之后执行expire之前进程意外crash或者要重启维护了，那会怎么样？

这时候你要给予惊讶的反馈：唉，是喔，这个锁就永远得不到释放了。紧接着你需要抓一抓自己得脑袋，故作思考片刻，好像接下来的结果是你主动思考出来的，然后回我记得set指令有非常复杂的参数，这个应该是可以同时把setnx和expire合成一条指令来用的！对方这时会显露笑容，心里开始默念：摁，这小子还不错。


### [8、Reids主从复制](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#8reids主从复制)  


复制是高可用Redis的基础，哨兵和集群都是在复制基础上实现高可用的。复制主要实现了数据的多机备份，以及对于读操作的负载均衡和简单的故障恢复。缺陷：故障恢复无法自动化；写操作无法负载均衡；存储能力受到单机的限制。


### [9、Redis与Memcached相比有哪些优势？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#9redis与memcached相比有哪些优势)  


**1、** Memcached所有的值均是简单的字符串，Redis作为其替代者，支持更为丰富的数据类型

**2、** Redis的速度比Memcached快很多Redis的速度比Memcached快很多

**3、** Redis可以持久化其数据Redis可以持久化其数据


### [10、Redis 最适合的场景？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新2021年面试题及答案，汇总版.md#10redis-最适合的场景)  


**1、** 会话缓存（ Session  Cache）

最常用的一种使用 Redis 的情景是会话缓存（ session cache）。用 Redis 缓存会话比其他存储（ 如 Memcached）的优势在于：Redis 提供持久化。当维护一个不是严格要求一致性的缓存时， 如果用户的购物车信息全部丢失， 大部分人都会不高兴的， 现在， 他们还会这样吗？ 幸运的是， 随着 Redis 这些年的改进， 很容易找到怎么恰当的使用 Redis 来缓存会话的文档。甚至广为人知的商业平台Magento 也提供 Redis 的插件。

**2、** 全页缓存（ FPC）

除基本的会话 token 之外， Redis 还提供很简便的 FPC 平台。回到一致性问题， 即使重启了 Redis 实例， 因为有磁盘的持久化， 用户也不会看到页面加载速度的下降，这是一个极大改进，类似 PHP 本地 FPC。 再次以 Magento 为例，Magento 提供一个插件来使用 Redis 作为全页缓存后端。 此外， 对 WordPress 的用户来说， Pantheon 有一个非常好的插件 wp-Redis， 这个插件能帮助你以最快速度加载你曾浏览过的页面。

3、队列

Reids 在内存存储引擎领域的一大优点是提供 list 和 set 操作， 这使得 Redis 能作为一个很好的消息队列平台来使用。Redis 作为队列使用的操作，就类似于本地程序语言（ 如 Python）对 list 的 push/pop 操作。 如果你快速的在 Google 中搜索“ Redis  queues”， 你马上就能找到大量的开源项目， 这些项目的目的就是利用 Redis 创建非常好的后端工具， 以满足各种队列需求。例如， Celery 有一个后台就是使用 Redis 作为 broker， 你可以从这里去查看。

4， 排行榜/计数器

Redis 在内存中对数字进行递增或递减的操作实现的非常好。集合（ Set） 和有序集合（ Sorted Set）也使得我们在执行这些操作的时候变的非常简单，Redis 只是正好提供了这两种数据结构。所以， 我们要从排序集合中获取到排名最靠前的 10 个用户– 我们称之为“ user_scores”， 我们只需要像下面一样执行即可：   当然，这是假定你是根据你用户的分数做递增的排序。如果你想返回用户及用户的分数，   你需要这样执行：  ZRANGE user_scores 0 10 WITHSCORES Agora Games 就是一个很好的例子， 用 Ruby 实现的， 它的排行榜就是使用 Redis 来存储数据的， 你可以在这里看到。

**5、** 发布/订阅

最后（ 但肯定不是最不重要的）是 Redis 的发布/订阅功能。发布/订阅的使用场景确实非常多。我已看见人们在社交网络连接中使用， 还可作为基于发布/订阅的脚本触发器， 甚至用 Redis 的发布/订阅功能来建立聊天系统！


### 11、Redis对象有5种类型
### 12、Redis回收进程如何工作的？
### 13、Redis中的管道有什么用？
### 14、Reids持久化触发条件
### 15、Memcache与Redis的区别都有哪些？
### 16、Redis的同步机制了解么？
### 17、Redis 最适合的场景
### 18、如果有大量的 key 需要设置同一时间过期，一般需要注意什么？
### 19、使用过 Redis 做异步队列么，你是怎么用的？
### 20、Redis相比Memcached有哪些优势？
### 21、都有哪些办法可以降低Redis的内存使用情况呢？
### 22、Redis主要消耗什么物理资源？
### 23、Redis事物的了解CAS(check-and-set 操作实现乐观锁 )?
### 24、为什么Redis需要把所有数据放到内存中?
### 25、MySQL里有2000w数据，Redis中只存20w的数据，如何保证Redis中的数据都是热点数据？
### 26、SCAN系列命令注意事项
### 27、Redis 集群的主从复制模型是怎样的？
### 28、读写分离模型
### 29、Redis 开启AOF





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




