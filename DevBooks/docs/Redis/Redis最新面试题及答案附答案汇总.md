# Redis最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、MySQL里有2000w数据，Redis中只存20w的数据，如何保证Redis中的数据都是热点数据？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#1mysql里有2000w数据redis中只存20w的数据如何保证redis中的数据都是热点数据)  


Redis内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。


### [2、Redis 过期键的删除策略？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#2redis-过期键的删除策略)  


**1、** 定时删除:在设置键的过期时间的同时，创建一个定时器 timer). 让定时器在键的过期时间来临时， 立即执行对键的删除操作。

**2、** 惰性删除:放任键过期不管，但是每次从键空间中获取键时，都检查取得的键是   否过期， 如果过期的话， 就删除该键;如果没有过期， 就返回该键。

**3、** 定期删除:每隔一段时间程序就对数据库进行一次检查，删除里面的过期键。至   于要删除多少过期键， 以及要检查多少个数据库， 则由算法决定。


### [3、mySQL里有2000w数据，Redis中只存20w的数据，如何保证Redis中的数据都是热点数据](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#3mysql里有2000w数据redis中只存20w的数据如何保证redis中的数据都是热点数据)  


_相关知识：Redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略（回收策略）。_


### [4、Redis key的过期时间和永久有效分别怎么设置？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#4redis-key的过期时间和永久有效分别怎么设置)  


EXPIRE和PERSIST命令。


### [5、请用Redis和任意语言实现一段恶意登录保护的代码，](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#5请用redis和任意语言实现一段恶意登录保护的代码)  


限制1小时内每用户Id最多只能登录5次。具体登录函数或功能用空函数即可，不用详细写出。

用列表实现:列表中每个元素代表登陆时间,只要最后的第5次登陆时间和现在时间差不超过1小时就禁止登陆.用Python写的代码如下：

```
#!/usr/bin/env python3
import Redis  
import sys  
import time  
 
r = Redis.StrictRedis(host=’127.0.0.1′, port=6379, db=0)  
try:       
    id = sys.argv[1]
except:      
    print(‘input argument error’)    
    sys.exit(0)  
if r.llen(id) >= 5 and time.time() – float(r.lindex(id, 4)) <= 3600:      
    print(“you are forbidden logining”)
else:       
    print(‘you are allowed to login’)    
    r.lpush(id, time.time())    
    # login_func()
```


### [6、，或是关注](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#6或是关注)  

### [7、怎么理解Redis事务？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#7怎么理解redis事务)  




事务是一个单独的隔离操作：事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。

事务是一个原子操作：事务中的命令要么全部被执行，要么全部都不执行。


### [8、Redis key 的过期时间和永久有效分别怎么设置？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#8redis-key-的过期时间和永久有效分别怎么设置)  


EXPIRE 和 PERSIST 命令。


### [9、Redis中海量数据的正确操作方式](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#9redis中海量数据的正确操作方式)  


利用SCAN系列命令（SCAN、SSCAN、HSCAN、ZSCAN）完成数据迭代。


### [10、什么是Redis？简述它的优缺点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Redis/Redis最新面试题及答案附答案汇总.md#10什么是redis简述它的优缺点)  


Redis的全称是：Remote Dictionary.Server，本质上是一个Key-Value类型的内存数据库，很像Memcached，整个数据库统统加载在内存当中进行操作，定期通过异步操作把数据库数据flush到硬盘上进行保存。

因为是纯内存操作，Redis的性能非常出色，每秒可以处理超过 10万次读写操作，是已知性能最快的Key-Value DB。

Redis的出色之处不仅仅是性能，Redis最大的魅力是支持保存多种数据结构，此外单个value的最大限制是1GB，不像 Memcached只能保存1MB的数据，因此Redis可以用来实现很多有用的功能。

比方说用他的List来做FIFO双向链表，实现一个轻量级的高性 能消息队列服务，用他的Set可以做高性能的tag系统等等。

另外Redis也可以对存入的Key-Value设置expire时间，因此也可以被当作一 个功能加强版的Memcached来用。 Redis的主要缺点是数据库容量受到物理内存的限制，不能用作海量数据的高性能读写，因此Redis适合的场景主要局限在较小数据量的高性能操作和运算上。


### 11、Redis如何做内存优化？
### 12、Redis 集群如何选择数据库？
### 13、定期删除
### 14、内存碎片
### 15、Redis 集群之间是如何复制的？
### 16、数据分片模型
### 17、Jedis与Redisson对比有什么优缺点？
### 18、Redis事务相关的命令有哪几个？
### 19、使用过Redis做异步队列么，你是怎么用的？
### 20、什么是Redis?
### 21、Redis持久化的几种方式
### 22、Redis回收进程如何工作的？
### 23、Redis有哪些适合的场景？
### 24、Redis集群如何选择数据库？
### 25、Redis常见性能问题和解决方案：
### 26、使用Redis 有哪些好处？
### 27、Redis的回收策略（淘汰策略）?
### 28、Jedis与Redisson对比有什么优缺点？
### 29、进程本身运行需要的内存





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




