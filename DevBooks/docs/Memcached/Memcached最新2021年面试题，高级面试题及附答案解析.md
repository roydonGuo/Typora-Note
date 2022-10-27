# Memcached最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Memcached的多线程是什么？如何使用它们？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#1memcached的多线程是什么如何使用它们)  


线程就是定律（threads rule）！在Steven Grimm和Facebook的努力下，Memcached 1.2及更高版本拥有了多线程模式。多线程模式允许Memcached能够充分利用多个CPU，并在CPU之间共享所有的缓存数据。Memcached使用一种简单的锁机制来保证数据更新操作的互斥。相比在同一个物理机器上运行多个Memcached实例，这种方式能够更有效地处理multi gets。

如果您的系统负载并不重，也许您不需要启用多线程工作模式。如果您在运行一个拥有大规模硬件的、庞大的网站，您将会看到多线程的好处。

简单地总结一下：命令解析（Memcached在这里花了大部分时间）可以运行在多线程模式下。Memcached内部对数据的操作是基于很多全局锁的（因此这部分工作不是多线程的）。未来对多线程模式的改进，将移除大量的全局锁，提高Memcached在负载极高的场景下的性能。


### [2、Memcached是什么，有什么作用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#2memcached是什么有什么作用)  


Memcached是一个开源的，高性能的内存绶存软件，从名称上看Mem就是内存的意思，而Cache就是缓存的意思。Memcached的作用：通过在事先规划好的内存空间中临时绶存数据库中的各类数据，以达到减少业务对数据库的直接高并发访问，从而达到提升数据库的访问性能，加速网站集群动态应用服务的能力。


### [3、Memcached与Redis的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#3memcached与redis的区别)  


**1、** Redis不仅仅支持简单的k/v类型的数据，同时还提供list，set，zset，hash等数据结构的存储。而memcache只支持简单数据类型，需要客户端自己处理复杂对象

**2、** Redis支持数据的持久化，可以将内存中的数据保持在磁盘中，重启的时候可以再次加载进行使用（PS：持久化在rdb、aof）。

**3、** 由于Memcache没有持久化机制，因此宕机所有缓存数据失效。Redis配置为持久化，宕机重启后，将自动加载宕机时刻的数据到缓存系统中。具有更好的灾备机制。

**4、** Memcache可以使用Magent在客户端进行一致性hash做分布式。Redis支持在服务器端做分布式（PS:Twemproxy/Codis/Redis-cluster多种分布式实现方式）

**5、** Memcached的简单限制就是键（key）和Value的限制。最大键长为250个字符。可以接受的储存数据不能超过1MB（可修改配置文件变大），因为这是典型slab 的最大值，不适合虚拟机使用。而Redis的Key长度支持到512k。

**6、** Redis使用的是单线程模型，保证了数据按顺序提交。Memcache需要使用cas保证数据一致性。CAS（Check and Set）是一个确保并发一致性的机制，属于“乐观锁”范畴；原理很简单：拿版本号，操作，对比版本号，如果一致就操作，不一致就放弃任何操作

cpu利用。由于Redis只使用单核，而Memcached可以使用多核，所以平均每一个核上Redis在存储小数据时比Memcached性能更 高。而在100k以上的数据中，Memcached性能要高于Redis 。

**7、** memcache内存管理：使用Slab Allocation。原理相当简单，预先分配一系列大小固定的组，然后根据数据大小选择最合适的块存储。避免了内存碎片。（缺点：不能变长，浪费了一定空间）Memcached默认情况下下一个slab的最大值为前一个的1.25倍。

**8、** Redis内存管理： Redis通过定义一个数组来记录所有的内存分配情况， Redis采用的是包装的malloc/free，相较于Memcached的内存 管理方法来说，要简单很多。由于malloc 首先以链表的方式搜索已管理的内存中可用的空间分配，导致内存碎片比较多

### [4、什么是二进制协议，我该关注吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#4什么是二进制协议我该关注吗)  


**关于二进制最好的信息当然是二进制协议规范：**

二进制协议尝试为端提供一个更有效的、可靠的协议，减少客户端/服务器端因处理协议而产生的CPU时间。

根据Facebook的测试，解析ASCII协议是Memcached中消耗CPU时间最多的环节。所以，我们为什么不改进ASCII协议呢？


### [5、如果缓存数据在导出导入之间过期了，您又怎么处理这些数据呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#5如果缓存数据在导出导入之间过期了您又怎么处理这些数据呢)  


因此，批量导出导入数据并不像您想象中的那么有用。不过在一个场景倒是很有用。如果您有大量的从不变化的数据，并且希望缓存很快热（warm）起来，批量导入缓存数据是很有帮助的。虽然这个场景并不典型，但却经常发生，因此我们会考虑在将来实现批量导出导入的功能。

如果一个Memcached节点down了让您很痛苦，那么您还会陷入其他很多麻烦。您的系统太脆弱了。您需要做一些优化工作。比如处理”惊群”问题（比如 Memcached节点都失效了，反复的查询让您的数据库不堪重负…这个问题在FAQ的其他提到过），或者优化不好的查询。记住，Memcached 并不是您逃避优化查询的借口。


### [6、如何实现集群中的session共享存储？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#6如何实现集群中的session共享存储)  


Session是运行在一台服务器上的，所有的访问都会到达我们的唯一服务器上，这样我们可以根据客户端传来的sessionID，来获取session，或在对应Session不存在的情况下（session 生命周期到了/用户第一次登录），创建一个新的Session；但是，如果我们在集群环境下，假设我们有两台服务器A，B，用户的请求会由Nginx服务器进行转发（别的方案也是同理），用户登录时，Nginx将请求转发至服务器A上，A创建了新的session，并将SessionID返回给客户端，用户在浏览其他页面时，客户端验证登录状态，Nginx将请求转发至服务器B，由于B上并没有对应客户端发来sessionId的session，所以会重新创建一个新的session，并且再将这个新的sessionID返回给客户端，这样，我们可以想象一下，用户每一次操作都有1/2的概率进行再次的登录，这样不仅对用户体验特别差，还会让服务器上的session激增，加大服务器的运行压力。

**为了解决集群环境下的seesion共享问题，共有4种解决方案：**

**1、** 粘性session

粘性session是指Ngnix每次都将同一用户的所有请求转发至同一台服务器上，即将用户与服务器绑定。

**2、** 服务器session复制

即每次session发生变化时，创建或者修改，就广播给所有集群中的服务器，使所有的服务器上的session相同。

**3、** session共享

缓存session，使用Redis， Memcached。

**4、** session持久化

将session存储至数据库中，像操作数据一样才做session。


### [7、Memcached和MySQL的query](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#7memcached和mysql的query)  


**cache相比，有什么优缺点？**

把Memcached引入应用中，还是需要不少工作量的。MySQL有个使用方便的query cache，可以自动地缓存SQL查询的结果，被缓存的SQL查询可以被反复地快速执行。Memcached与之相比，怎么样呢？MySQL的query cache是集中式的，连接到该query cache的MySQL服务器都会受益。

**1、** 当您修改表时，MySQL的query cache会立刻被刷新（flush）。存储一个Memcached item只需要很少的时间，但是当写操作很频繁时，MySQL的query cache会经常让所有缓存数据都失效。

**2、** 在多核CPU上，MySQL的query cache会遇到扩展问题（scalability issues）。在多核CPU上，query cache会增加一个全局锁（global lock）, 由于需要刷新更多的缓存数据，速度会变得更慢。

**3、** 在 MySQL的query cache中，我们是不能存储任意的数据的（只能是SQL查询结果）。而利用Memcached，我们可以搭建出各种高效的缓存。比如，可以执行多个独立的查询，构建出一个用户对象（user object），然后将用户对象缓存到Memcached中。而query cache是SQL语句级别的，不可能做到这一点。在小的网站中，query cache会有所帮助，但随着网站规模的增加，query cache的弊将大于利。

**4、** query cache能够利用的内存容量受到MySQL服务器空闲内存空间的限制。给数据库服务器增加更多的内存来缓存数据，固然是很好的。但是，有了Memcached，只要您有空闲的内存，都可以用来增加Memcached集群的规模，然后您就可以缓存更多的数据。


### [8、Memcached是原子的吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#8memcached是原子的吗)  


所有的被发送到Memcached的单个命令是完全原子的。如果您针对同一份数据同时发送了一个set命令和一个get命令，它们不会影响对方。它们将被串行化、先后执行。即使在多线程模式，所有的命令都是原子的，除非程序有bug:)

命令序列不是原子的。如果您通过get命令获取了一个item，修改了它，然后想把它set回Memcached，我们不保证这个item没有被其他进程（process，未必是操作系统中的进程）操作过。在并发的情况下，您也可能覆写了一个被其他进程set的item。

Memcached 1.2.5以及更高版本，提供了gets和cas命令，它们可以解决上面的问题。如果您使用gets命令查询某个key的item，Memcached会给您返回该item当前值的唯一标识。如果您覆写了这个item并想把它写回到Memcached中，您可以通过cas命令把那个唯一标识一起发送给 Memcached。如果该item存放在Memcached中的唯一标识与您提供的一致，您的写操作将会成功。如果另一个进程在这期间也修改了这个 item，那么该item存放在Memcached中的唯一标识将会改变，您的写操作就会失败


### [9、Memcached能够更有效地使用内存吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#9memcached能够更有效地使用内存吗)  


Memcache客户端仅根据哈希算法来决定将某个key存储在哪个节点上，而不考虑节点的内存大小。因此，您可以在不同的节点上使用大小不等的缓存。但是一般都是这样做的：拥有较多内存的节点上可以运行多个Memcached实例，每个实例使用的内存跟其他节点上的实例相同。


### [10、Memcached的内存分配器是如何工作的？为什么不适用malloc/free！？为何要使用slabs？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Memcached/Memcached最新2021年面试题，高级面试题及附答案解析.md#10memcached的内存分配器是如何工作的为什么不适用malloc/free为何要使用slabs)  


实际上，这是一个编译时选项。默认会使用内部的slab分配器。您确实确实应该使用内建的slab分配器。最早的时候，Memcached只使用 malloc/free来管理内存。然而，这种方式不能与OS的内存管理以前很好地工作。反复地malloc/free造成了内存碎片，OS最终花费大量的时间去查找连续的内存块来满足malloc的请求，而不是运行Memcached进程。如果您不同意，当然可以使用malloc！只是不要在邮件列表中抱怨啊

slab分配器就是为了解决这个问题而生的。内存被分配并划分成chunks，一直被重复使用。因为内存被划分成大小不等的slabs，如果item 的大小与被选择存放它的slab不是很合适的话，就会浪费一些内存。Steven Grimm正在这方面已经做出了有效的改进。


### 11、Memcached是怎么工作的？
### 12、Memcached的cache机制是怎样的？
### 13、Memcached能接受的key的最大长度是多少？
### 14、Memcached服务特点及工作原理是什么？
### 15、Memcached和服务器的local cache（比如PHP的APC、mmap文件等）相比，有什么优缺点？
### 16、Memcached如何处理容错的？
### 17、Memcached是如何做身份验证的？
### 18、简述Memcached内存管理机制原理？
### 19、Memcached最大能存储多大的单个item？
### 20、Memcached如何实现冗余机制？
### 21、如何将Memcached中item批量导入导出？
### 22、Memcached服务在企业集群架构中有哪些应用场景？
### 23、Memcached最大的优势是什么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




