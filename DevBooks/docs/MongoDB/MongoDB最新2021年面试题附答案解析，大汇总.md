# MongoDB最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、我怎么查看 Mongo 正在使用的链接？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#1我怎么查看-mongo-正在使用的链接)  


db._adminCommand("connPoolStats");


### [2、数据库的整体结构](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#2数据库的整体结构)  


键值对–》文档–》集合–》数据库



### [3、在MongoDB中如何排序](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#3在mongodb中如何排序)  


并使用 1 和 -1 来指定排序方式，其中 1 表示升序，而 -1 表示降序。

db.connectionName.find({key:value}).sort({columnName:1})


### [4、getLastError的作用](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#4getlasterror的作用)  


调用getLastError 可以确认当前的写操作是否成功的提交


### [5、启用备份故障恢复需要多久?](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#5启用备份故障恢复需要多久)  


从备份数据库声明主数据库宕机到选出一个备份数据库作为新的主数据库将花费10到30秒时间.这期间在主数据库上的操作将会失败–包括写入和强一致性读取(strong consistent read)操作.然而,你还能在第二数据库上执行最终一致性查询(eventually consistent query)(在slaveok模式下),即使在这段时间里.


### [6、mongodb是否支持事务](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#6mongodb是否支持事务)  


MongoDB 4.0的新特性——事务（Transactions）：MongoDB 是不支持事务的，因此开发者在需要用到事务的时候，不得不借用其他工具，在业务代码层面去弥补数据库的不足。

事务和会话(Sessions)关联，一个会话同一时刻只能开启一个事务操作，当一个会话断开，这个会话中的事务也会结束。



### [7、提及Objecld由什么组成？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#7提及objecld由什么组成)  


**Objectld由以下组成**

**1、** 时间戳记

**2、** 客户端机器ID

**3、** 客户端进程ID

**4、** 3字节递增计数器


### [8、在MongoDB中创建集合并将其删除的语法是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#8在mongodb中创建集合并将其删除的语法是什么)  


**1、** 在MongoDB中创建集合的语法是db.createCollection（name，options）

**2、** 在MongoDB中删除收集的语法是db.collection.drop（）


### [9、MongoDB中的命名空间是什么意思?](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#9mongodb中的命名空间是什么意思)  


mongodb存储bson对象在丛集(collection)中.数据库名字和丛集名字以句点连结起来叫做名字空间(namespace). 一个集合命名空间又有多个数据域(extent)，集合命名空间里存储着集合的元数据，比如集合名称，集合的

第一个数据域和最后一个数据域的位置等等。而一个数据域由若干条文档(document)组成，每个数据域都有一个

头部，记录着第一条文档和最后一条文档的为知，以及该数据域的一些元数据。extent之间，document之间通过

双向链表连接。 索引的存储数据结构是B树，索引命名空间存储着对B树的根节点的指针。


### [10、MongoDB在A:{B,C}上建立索引，查询A:{B,C}和A:{C,B}都会使用索引吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MongoDB/MongoDB最新2021年面试题附答案解析，大汇总.md#10mongodb在a:{b,c}上建立索引查询a:{b,c}和a:{c,b}都会使用索引吗)  


不会，只会在A:{B,C}上使用索引。


### 11、数据在什么时候才会扩展到多个分片（shard）里？
### 12、MongoDB中的分片是什么？
### 13、如何删除文档
### 14、更新操作立刻fsync到磁盘？
### 15、当我试图更新一个正在被迁移的块（chunk）上的文档时会发生什么？
### 16、什么是非关系型数据库
### 17、分片(sharding)和复制(replication)是怎样工作的?
### 18、MongoDB相似的产品有哪些？
### 19、什么是MongoDB
### 20、在哪些场景使用MongoDB
### 21、如果块移动操作(movechunk)失败了,我需要手动清除部分转移的文档吗?
### 22、什么是聚合
### 23、什么是master或primary?
### 24、31如何理解MongoDB中的GridFS机制，MongoDB为何使用GridFS来存储文件？
### 25、查看是否在主服务器上的命令语法是什么？MongoDB允许多少个主机？
### 26、用什么方法可以格式化输出结果
### 27、解释一下您可以将旧文件移动到moveChunk目录中吗？
### 28、数据在什么时候才会扩展到多个分片(shard)里?
### 29、什么是数据库





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




