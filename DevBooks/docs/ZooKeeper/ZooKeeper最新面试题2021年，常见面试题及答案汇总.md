# ZooKeeper最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Zookeeper 下 Server工作状态](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#1zookeeper-下-server工作状态)  


每个Server在工作过程中有三种状态：

LOOKING：当前Server不知道leader是谁，正在搜寻

LEADING：当前Server即为选举出来的leader

FOLLOWING：leader已经选举出来，当前Server与之同步


### [2、ZooKeeper定义了几种权限？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#2zookeeper定义了几种权限)  


**1、** CREATE

**2、** READ

**3、** WRITE

**4、** DELETE

**5、** ADMIN


### [3、ZooKeeper用推/拉模式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#3zookeeper用推/拉模式)  


推拉结合


### [4、客户端如何获取配置信息？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#4客户端如何获取配置信息)  


启动时主动到服务端拉取信息，同时，在制定节点注册Watcher监听。一旦有配置变化，服务端就会实时通知订阅它的所有客户端。

### [5、会话管理](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#5会话管理)  


分桶策略：将类似的会话放在同一区块中进行管理，以便于 Zookeeper 对会话进行不同区块的隔离处理以及同一区块的统一处理。

分配原则：每个会话的“下次超时时间点”（ExpirationTime）

**计算公式：**

```
ExpirationTime\_ = currentTime + sessionTimeout

ExpirationTime = (ExpirationTime\_ / ExpirationInrerval + 1) \*

ExpirationInterval , ExpirationInterval 是指 Zookeeper 会话超时检查时间间隔，默认 tickTime
```


### [6、四种类型的数据节点 Znode](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#6四种类型的数据节点-znode)  


**1、** PERSISTENT-持久节点 除非手动删除，否则节点一直存在于 Zookeeper 上

**2、** EPHEMERAL-临时节点 临时节点的生命周期与客户端会话绑定，一旦客户端会话失效（客户端与zookeeper 连接断开不一定会话失效），那么这个客户端创建的所有临时节点都会被移除。

**3、** PERSISTENT_SEQUENTIAL-持久顺序节点 基本特性同持久节点，只是增加了顺序属性，节点名后边会追加一个由父节点维护的自增整型数字。

**4、** EPHEMERAL_SEQUENTIAL-临时顺序节点 基本特性同临时节点，增加了顺序属性，节点名后边会追加一个由父节点维护的自增整型数字。


### [7、zookeeper是如何保证事务的顺序一致性的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#7zookeeper是如何保证事务的顺序一致性的)  


zookeeper采用了递增的事务Id来标识，所有的proposal（提议）都在被提出的时候加上了zxid，zxid实际上是一个64位的数字，高32位是epoch（时期; 纪元; 世; 新时代）用来标识leader是否发生改变，如果有新的leader产生出来，epoch会自增，低32位用来递增计数。当新产生proposal的时候，会依据数据库的两阶段过程，首先会向其他的server发出事务执行请求，如果超过半数的机器都能执行并且能够成功，那么就会开始执行。


### 8、发现?

Follower把自己最后的接受事务的Proposal值(CEPOCH(F.p)发送给Leader。

当收到过半Follower的消息后，Leader生成NEWEPOCH(e')给这些过半的Follower。

tips: e' = Max((CEPOCH(F.p)) + 1

Follower收到消息后，如果自己值小于e',则同步e'的值，同时向Leader发Ack消息。


### [9、客户端注册Watcher实现](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#9客户端注册watcher实现)  


**1、** 调用getData()/getChildren()/exist()三个API，传入Watcher对象

**2、** 标记请求request，封装Watcher到WatchRegistration

**3、** 封装成Packet对象，发服务端发送request

**4、** 收到服务端响应后，将Watcher注册到ZKWatcherManager中进行管理

**5、** 请求返回，完成注册。


### [10、Zookeeper文件系统](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新面试题2021年，常见面试题及答案汇总.md#10zookeeper文件系统)  


Zookeeper提供一个多层级的节点命名空间（节点称为znode）。与文件系统不同的是，这些节点都可以设置关联的数据，而文件系统中只有文件节点可以存放数据而目录节点不行。Zookeeper为了保证高吞吐和低延迟，在内存中维护了这个树状的目录结构，这种特性使得Zookeeper不能用于存放大量的数据，每个节点的存放数据上限为1M。


### 11、Zookeeper有哪几种几种部署模式？
### 12、Zookeeper做了什么？
### 13、chubby 是什么，和 zookeeper 比你怎么看？
### 14、权限控制?
### 15、Zookeeper工作原理
### 16、说一下 Zookeeper 的通知机制？
### 17、ZAB的两种基本模式？
### 18、分布式集群中为什么会有Master？
### 19、四种类型的znode
### 20、Zookeeper 下 Server 工作状态
### 21、Zookeeper的典型应用场景
### 22、Zookeeper Watcher 机制 -- 数据变更通知
### 23、会话管理
### 24、集群角色？
### 25、Zookeeper 和 Dubbo 的关系？
### 26、zookeeper是如何保证事务的顺序一致性的？
### 27、ZAB三个阶段？
### 28、Zookeeper 下 Server工作状态
### 29、获取指定节点信息？
### 30、分布式通知和协调





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




