# ZooKeeper最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Stat记录了哪些版本相关数据？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#1stat记录了哪些版本相关数据)  


version:当前ZNode版本

cversion:当前ZNode子节点版本

aversion:当前ZNode的ACL版本


### [2、BASE理论？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#2base理论)  


**1、** Basically Available(基本可用)、Soft state(软状态) 和 Eventuanlly consistent （最终一致性）3个短语的简写。

**2、** 基本可用：系统出现不可预知的故障时，允许损失部分可用性。

**3、** 弱（软）状态：数据的中间状态，并认为改状态存在不会一项系统整体可用性，允许不同节点数据副本数据同步过程中的延时。

**4、** 最终一致性：系统中所有数据副本，在一段时间的同步后，最终数据能够到一致性的状态。


### [3、Zookeeper Watcher 机制 – 数据变更通知](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#3zookeeper-watcher-机制-–-数据变更通知)  


Zookeeper 允许客户端向服务端的某个 Znode 注册一个 Watcher 监听，当服务端的一些指定事件触发了这个 Watcher，服务端会向指定客户端发送一个事件通知来实现分布式的通知功能，然后客户端根据 Watcher 通知状态和事件类型做出业务上的改变。

**工作机制：**

**1、** 客户端注册 watcher

**2、** 服务端处理 watcher

**3、** 客户端回调 watcher


### [4、如何识别请求的先后顺序？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#4如何识别请求的先后顺序)  


ZooKeeper会给每个更新请求，分配一个全局唯一的递增编号（zxid)，编号的大小体现事务操作的先后顺序。


### [5、zk的命名服务（文件系统）](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#5zk的命名服务文件系统)  


命名服务是指通过指定的名字来获取资源或者服务的地址，利用zk创建一个全局的路径，即是唯一的路径，这个路径就可以作为一个名字，指向集群中的集群，提供的服务的地址，或者一个远程的对象等等。


### [6、如何查看子节点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#6如何查看子节点)  


ls path [watch]

path : 节点路径

[zk: localhost:2181(CONNECTED) 5] ls /app

[book]


### [7、chubby是什么，和zookeeper比你怎么看？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#7chubby是什么和zookeeper比你怎么看)  


chubby是google的，完全实现paxos算法，不开源。zookeeper是chubby的开源实现，使用zab协议，paxos算法的变种。


### [8、ZooKeeper 面试题？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#8zookeeper-面试题)  


ZooKeeper是一个开放源码的分布式协调服务，它是集群的管理者，监视着集群中各个节点的状态根据节点提交的反馈进行下一步合理操作。最终，将简单易用的接口和性能高效、功能稳定的系统提供给用户。

分布式应用程序可以基于Zookeeper实现诸如数据发布/订阅、负载均衡、命名服务、分布式协调/通知、集群管理、Master选举、分布式锁和分布式队列等功能。

**Zookeeper保证了如下分布式一致性特性：**

**1、** 顺序一致性

**2、** 原子性

**3、** 单一视图

**4、** 可靠性

**5、** 实时性（最终一致性）

客户端的读请求可以被集群中的任意一台机器处理，如果读请求在节点上注册了监听器，这个监听器也是由所连接的zookeeper机器来处理。对于写请求，这些请求会同时发给其他zookeeper机器并且达成一致后，请求才会返回成功。因此，随着zookeeper的集群机器增多，读请求的吞吐会提高但是写请求的吞吐会下降。

有序性是zookeeper中非常重要的一个特性，所有的更新都是全局有序的，每个更新都有一个唯一的时间戳，这个时间戳称为zxid（Zookeeper Transaction Id）。而读请求只会相对于更新有序，也就是读请求的返回结果中会带有这个zookeeper最新的zxid。


### [9、Zookeeper 有哪几种几种部署模式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#9zookeeper-有哪几种几种部署模式)  


**Zookeeper 有三种部署模式**：

**1、** 单机部署：一台集群上运行；

**2、** 集群部署：多台集群运行；

**3、** 伪集群部署：一台集群启动多个 Zookeeper 实例运行。


### [10、服务端处理Watcher实现](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题大汇总，附答案.md#10服务端处理watcher实现)  


**1、** 服务端接收Watcher并存储

接收到客户端请求，处理请求判断是否需要注册Watcher，需要的话将数据节点的节点路径和ServerCnxn（ServerCnxn代表一个客户端和服务端的连接，实现了Watcher的process接口，此时可以看成一个Watcher对象）存储在WatcherManager的WatchTable和watch2Paths中去。

**2、** Watcher触发

以服务端接收到 setData() 事务请求触发NodeDataChanged事件为例：

2.1 封装WatchedEvent

将通知状态（SyncConnected）、事件类型（NodeDataChanged）以及节点路径封装成一个WatchedEvent对象

2.2 查询Watcher

从WatchTable中根据节点路径查找Watcher

2.3 没找到；说明没有客户端在该数据节点上注册过Watcher

2.4 找到；提取并从WatchTable和Watch2Paths中删除对应Watcher（从这里可以看出Watcher在服务端是一次性的，触发一次就失效了）

**3、** 调用process方法来触发Watcher

这里process主要就是通过ServerCnxn对应的TCP连接发送Watcher事件通知。


### 11、客户端注册 Watcher 实现
### 12、客户端回调 Watcher
### 13、为什么叫ZooKeeper?
### 14、在sessionTimeout之内的会话，因服务器压力大、网络故障或客户端主动断开情况下，之前的会话还有效吗？
### 15、Zookeeper 的典型应用场景
### 16、Zookeeper默认端口？
### 17、Zookeeper 都有哪些功能？
### 18、Zookeeper集群管理（文件系统、通知机制）
### 19、删除指定节点？注意？
### 20、CAP理论？
### 21、恢复模式
### 22、Quorum?
### 23、ZooKeeper是什么？
### 24、Zookeeper的java客户端都有哪些？
### 25、ZNode的类型？
### 26、集群最少要几台机器，集群规则是怎样的?
### 27、Zookeeper文件系统
### 28、ZooKeeper 提供了什么？
### 29、A是根节点，如何表达A子节点下的B节点？
### 30、Zookeeper队列管理（文件系统、通知机制）





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




