# Elasticsearch最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、elasticsearch的倒排索引是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#1elasticsearch的倒排索引是什么)  


`面试官`：想了解你对基础概念的认知。

通俗解释一下就可以。

传统的我们的检索是通过文章，逐个遍历找到对应关键词的位置。

而倒排索引，是通过分词策略，形成了词和文章的映射关系表，这种词典+映射表即为倒排索引。

有了倒排索引，就能实现`o（1）时间复杂度`的效率检索文章了，极大的提高了检索效率。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0814/01/img_2.png#alt=img%5C_2.png)

学术的解答方式：

> 倒排索引，相反于一篇文章包含了哪些词，它从词出发，记载了这个词在哪些文档中出现过，由两部分组成——词典和倒排表。


`加分项`：倒排索引的底层实现是基于：FST（Finite State Transducer）数据结构。

lucene从4+版本后开始大量使用的数据结构是FST。FST有两个优点：

**1、** 空间占用小。通过对词典中单词前缀和后缀的重复利用，压缩了存储空间；

**2、** 查询速度快。O(len(str))的查询时间复杂度。


### [2、Elasticsearch 在部署时，对 Linux 的设置有哪些优化方法](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#2elasticsearch-在部署时对-linux-的设置有哪些优化方法)  


面试官：想了解对 ES 集群的运维能力。

解

**1、** 关闭缓存 swap;

**2、** 堆内存设置为：Min（节点内存/2, 32GB）;

**3、** 设置最大文件句柄数；

**4、** 线程池+队列大小根据业务需要做调整；

**5、** 磁盘存储 raid 方式——存储有条件使用 RAID10，增加单节点性能以及避免单

节点存储故障。


### [3、详细描述一下Elasticsearch索引文档的过程](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#3详细描述一下elasticsearch索引文档的过程)  


`面试官`：想了解ES的底层原理，不再只关注业务层面了。

这里的索引文档应该理解为文档写入ES，创建索引的过程。

文档写入包含：单文档写入和批量bulk写入，这里只解释一下：单文档写入流程。

记住官方文档中的这个图。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0814/01/img_3.png#alt=img%5C_3.png)

第一步：客户写集群某节点写入数据，发送请求。（如果没有指定路由/协调节点，请求的节点扮演`路由节点`的角色。）

第二步：节点1接受到请求后，使用文档_id来确定文档属于分片0。请求会被转到另外的节点，假定节点3。因此分片0的主分片分配到节点3上。

第三步：节点3在主分片上执行写操作，如果成功，则将请求并行转发到节点1和节点2的副本分片上，等待结果返回。所有的副本分片都报告成功，节点3将向协调节点（节点1）报告成功，节点1向请求客户端报告写入成功。

如果面试官再问：第二步中的文档获取分片的过程？

回借助路由算法获取，路由算法就是根据路由和文档id计算目标的分片id的过程。

```
1shard = hash(_routing) % (num_of_primary_shards)
```


### [4、在并发情况下，Elasticsearch 如果保证读写一致？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#4在并发情况下elasticsearch-如果保证读写一致)  


**1、** 可以通过版本号使用乐观并发控制，以确保新版本不会被旧版本覆盖，**由应用**

**层来处理具体的冲突；**

**2、** 另外对于写操作，一致性级别支持 quorum/one/all，默认为 quorum，即只有当大多数分片可用时才允许写操作。但即使大多数可用，也可能存在因为网络等原因导致写入副本失败，这样该副本被认为故障，分片将会在一个不同的节点

上重建。

**3、** 对于读操作，可以设置 replication 为 sync(默认)，这使得操作在主分片和副本分片都完成后才会返回；如果设置 replication 为 async 时，也可以通过设置搜索请求参数_preference 为 primary 来查询主分片，确保文档是最新版本。


### [5、请解释在 Elasticsearch 集群中添加或创建索引的过程？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#5请解释在-elasticsearch-集群中添加或创建索引的过程)  


要添加新索引，应使用创建索引 API 选项。创建索引所需的参数是索引的配置Settings，索引中的字段 Mapping 以及索引别名 Alias。

也可以通过模板 Template 创建索引。


### [6、安装 Elasticsearch 需要依赖什么组件吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#6安装-elasticsearch-需要依赖什么组件吗)  


ES 早期版本需要JDK，在7.X版本后已经集成了 JDK，已无需第三方依赖。


### [7、如何使用 Elastic Reporting ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#7如何使用-elastic-reporting-)  


收费功能，只是了解，点到为止。

Reporting API有助于将检索结果生成 PD F格式，图像 PNG 格式以及电子表格 CSV 格式的数据，并可根据需要进行共享或保存。


### [8、elasticsearch 是如何实现 master 选举的](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#8elasticsearch-是如何实现-master-选举的)  


面试官：想了解 ES 集群的底层原理，不再只关注业务层面了。

解

**前置前提：**

**1、** 只有候选主节点（master：true）的节点才能成为主节点。

**2、** 最小主节点数（min_master_nodes）的目的是防止脑裂。

这个我看了各种网上分析的版本和源码分析的书籍，云里雾里。核对了一下代码，核心入口为 findMaster，选择主节点成功返回对应 Master，否则返回 null。

**选举流程大致描述如下：**

第一步：确认候选主节点数达标，elasticsearch.yml 设置的值

```
discovery.zen.minimum_master_nodes；
```

第二步：比较：先判定是否具备 master 资格，具备候选主节点资格的优先返回；

若两节点都为候选主节点，则 id 小的值会主节点。

注意这里的 id 为 string 类型。

题外话：获取节点 id 的方法。

```
1GET /_cat/nodes?v&h=ip,port,heapPercent,heapMax,id,name
2ip
port heapPercent heapMax id
name
```


### [9、在并发情况下，Elasticsearch如果保证读写一致？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#9在并发情况下elasticsearch如果保证读写一致)  


**1、** 可以通过版本号使用乐观并发控制，以确保新版本不会被旧版本覆盖，由应用层来处理具体的冲突；

**2、** 另外对于写操作，一致性级别支持quorum/one/all，默认为quorum，即只有当大多数分片可用时才允许写操作。但即使大多数可用，也可能存在因为网络等原因导致写入副本失败，这样该副本被认为故障，分片将会在一个不同的节点上重建。

**3、** 对于读操作，可以设置replication为sync(默认)，这使得操作在主分片和副本分片都完成后才会返回；如果设置replication为async时，也可以通过设置搜索请求参数_preference为primary来查询主分片，确保文档是最新版本。


### [10、详细描述一下Elasticsearch更新和删除文档的过程。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新2021年面试题，高级面试题及附答案解析.md#10详细描述一下elasticsearch更新和删除文档的过程。)  


**1、** 删除和更新也都是写操作，但是Elasticsearch中的文档是不可变的，因此不能被删除或者改动以展示其变更；

**2、** 磁盘上的每个段都有一个相应的.del文件。当删除请求发送后，文档并没有真的被删除，而是在.del文件中被标记为删除。该文档依然能匹配查询，但是会在结果中被过滤掉。当段合并时，在.del文件中被标记为删除的文档将不会被写入新段。

**3、** 在新的文档被创建时，Elasticsearch会为该文档指定一个版本号，当执行更新时，旧版本的文档在.del文件中被标记为删除，新版本的文档被索引到一个新段。旧版本的文档依然能匹配查询，但是会在结果中被过滤掉。


### 11、详细描述一下 Elasticsearch 更新和删除文档的过程。
### 12、在索引中更新 Mapping 的语法？
### 13、在Elasticsearch中 按 ID检索文档的语法是什么？
### 14、在 Elasticsearch 中删除索引的语法是什么？
### 15、详细描述一下Elasticsearch索引文档的过程。
### 16、Elasticsearch中的 Ingest 节点如何工作？
### 17、elasticsearch 索引数据多了怎么办，如何调优，部署
### 18、19、解释 Elasticsearch 中的相关性和得分？
### 19、ElasticSearch如何监控集群状态？
### 20、详细描述一下 Elasticsearch 索引文档的过程。
### 21、详细描述一下 Elasticsearch 搜索的过程？
### 22、定义副本、创建副本的好处是什么？
### 23、客户端在和集群连接时，如何选择特定的节点执行请求的？
### 24、您能否分步介绍如何启动 Elasticsearch 服务器？
### 25、Elasticsearch对于大数据量（上亿量级）的聚合如何实现？
### 26、Elasticsearch 中常用的 cat命令有哪些？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




