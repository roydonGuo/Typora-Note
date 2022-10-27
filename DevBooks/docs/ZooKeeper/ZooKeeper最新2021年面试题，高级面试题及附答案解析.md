# ZooKeeper最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、几种部署方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#1几种部署方式)  


单机、伪集群、集群


### [2、发布订阅的两种设计模式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#2发布订阅的两种设计模式)  


推(Push) :服务端主动推数据给所有定于的客户端。

拉(Pull):客户端主动发请求来获取最新数据。


### [3、服务端处理 Watcher 实现](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#3服务端处理-watcher-实现)  


**1、** 服务端接收 Watcher 并存储 接收到客户端请求，处理请求判断是否需要注册 Watcher，需要的话将数据节点的节点路径和 ServerCnxn（ServerCnxn 代表一个客户端和服务端的连接，实现了 Watcher 的 process 接口，此时可以看成一个 Watcher 对象）存储在WatcherManager 的 WatchTable 和 watch2Paths 中去。

**2、** Watcher 触发 以服务端接收到 setData() 事务请求触发 NodeDataChanged 事件为例：

2.1 封装 WatchedEvent 将通知状态（SyncConnected）、事件类型（NodeDataChanged）以及节点路径封装成一个 WatchedEvent 对象

2.2 查询 Watcher 从 WatchTable 中根据节点路径查找 Watcher

2.3 没找到；说明没有客户端在该数据节点上注册过 Watcher

2.4 找到；提取并从 WatchTable 和 Watch2Paths 中删除对应 Watcher（从这里可以看出 Watcher 在服务端是一次性的，触发一次就失效了）

**3、**  调用 process 方法来触发 Watcher 这里 process 主要就是通过 ServerCnxn 对应的 TCP 连接发送 Watcher 事件通知。


### [4、zk节点宕机如何处理？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#4zk节点宕机如何处理)  


Zookeeper本身也是集群，推荐配置不少于3个服务器。Zookeeper自身也要保证当一个节点宕机时，其他节点会继续提供服务。

如果是一个Follower宕机，还有2台服务器提供访问，因为Zookeeper上的数据是有多个副本的，数据并不会丢失；

如果是一个Leader宕机，Zookeeper会选举出新的Leader。

ZK集群的机制是只要超过半数的节点正常，集群就能正常提供服务。只有在ZK节点挂得太多，只剩一半或不到一半节点能工作，集群才失效。

所以

3个节点的cluster可以挂掉1个节点(leader可以得到2票>1.5)

2个节点的cluster就不能挂掉任何1个节点了(leader可以得到1票<=1)


### [5、Zookeeper 对节点的 watch 监听通知是永久的吗？为什么不是永久的?](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#5zookeeper-对节点的-watch-监听通知是永久的吗为什么不是永久的)  


**1、** 不是。官方声明：一个 Watch 事件是一个一次性的触发器，当被设置了 Watch的数据发生了改变的时候，则服务器将这个改变发送给设置了 Watch 的客户端，以便通知它们。

**2、** 为什么不是永久的，举个例子，如果服务端变动频繁，而监听的客户端很多情况下，每次变动都要通知到所有的客户端，给网络和服务器造成很大压力。

**3、** 一般是客户端执行 getData(“/节点 A”,true)，如果节点 A 发生了变更或删除，客户端会得到它的 watch 事件，但是在之后节点 A 又发生了变更，而客户端又没有设置 watch 事件，就不再给客户端发送。

**4、** 在实际应用中，很多情况下，我们的客户端不需要知道服务端的每一次变动，我只要最新的数据即可。


### [6、Zookeeper 怎么保证主从节点的状态同步？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#6zookeeper-怎么保证主从节点的状态同步)  


Zookeeper 的核心是原子广播机制，这个机制保证了各个 server 之间的同步。实现这个机制的协议叫做 Zab 协议。Zab 协议有两种模式，它们分别是恢复模式和广播模式。


### [7、数据发布/订阅](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#7数据发布/订阅)  


**介绍**

数据发布/订阅系统，即所谓的配置中心，顾名思义就是发布者发布数据供订阅者进行数据订阅。

**目的**

**1、** 动态获取数据（配置信息）

**2、** 实现数据（配置信息）的集中式管理和数据的动态更新

**设计模式**

**1、** Push 模式

**2、** Pull 模式

**数据（配置信息）特性**

**1、** 数据量通常比较小

**2、** 数据内容在运行时会发生动态更新

**3、** 集群中各机器共享，配置一致

如：机器列表信息、运行时开关配置、数据库配置信息等

**基于 Zookeeper 的实现方式**

**1、** 数据存储：将数据（配置信息）存储到 Zookeeper 上的一个数据节点

**2、** 数据获取：应用在启动初始化节点从 Zookeeper 数据节点读取数据，并在该节点上注册一个数据变更 Watcher

**3、** 数据变更：当变更数据时，更新 Zookeeper 对应节点数据，Zookeeper会将数据变更通知发到各客户端，客户端接到通知后重新读取变更后的数据即可。

#
### [8、同进程组的两个进程消息网络通信有哪两个特性？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#8同进程组的两个进程消息网络通信有哪两个特性)  


完整性： 如果进程a收到进程b的消息msg,那么b一定发送了消息msg。

前置性：如果msg1是msg2的前置消息，那么当前进程务必先接收到msg1,在接受msg2。


### [9、zookeeper 是如何保证事务的顺序一致性的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#9zookeeper-是如何保证事务的顺序一致性的)  


zookeeper 采用了全局递增的事务 Id 来标识，所有的 proposal（提议）都在被提出的时候加上了 zxid，zxid 实际上是一个 64 位的数字，高 32 位是 epoch（ 时期; 纪元; 世; 新时代）用来标识 leader 周期，如果有新的 leader 产生出来，epoch会自增，低 32 位用来递增计数。当新产生 proposal 的时候，会依据数据库的两阶段过程，首先会向其他的 server 发出事务执行请求，如果超过半数的机器都能执行并且能够成功，那么就会开始执行。


### [10、Chroot特性](https://gitee.com/souyunku/DevBooks/blob/master/docs/ZooKeeper/ZooKeeper最新2021年面试题，高级面试题及附答案解析.md#10chroot特性)  


3.2.0版本后，添加了 Chroot特性，该特性允许每个客户端为自己设置一个命名空间。如果一个客户端设置了Chroot，那么该客户端对服务器的任何操作，都将会被限制在其自己的命名空间下。

通过设置Chroot，能够将一个客户端应用于Zookeeper服务端的一颗子树相对应，在那些多个应用公用一个Zookeeper进群的场景下，对实现不同应用间的相互隔离非常有帮助。


### 11、四种类型的数据节点 Znode
### 12、客户端回调Watcher
### 13、zookeeper 负载均衡和 nginx 负载均衡区别
### 14、ACL 权限控制机制
### 15、Chroot 特性
### 16、获取分布式锁的流程
### 17、zookeeper负载均衡和nginx负载均衡区别
### 18、Zookeeper通知机制
### 19、数据同步
### 20、zookeeper watch机制
### 21、Zookeeper同步流程
### 22、zk 节点宕机如何处理？
### 23、Zookeeper分布式锁（文件系统、通知机制）
### 24、机器中为什么会有leader？
### 25、zk的配置管理（文件系统、通知机制）
### 26、更新指定节点信息？
### 27、如何创建一个ZNode?
### 28、Zookeeper数据复制
### 29、Watcher 特性总结
### 30、ZooKeeper可以实现哪些功能？
### 31、Zookeeper对节点的watch监听通知是永久的吗？为什么不是永久的?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




