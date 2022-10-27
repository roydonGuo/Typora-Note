# Elasticsearch最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Kibana在Elasticsearch的哪些地方以及如何使用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#1kibana在elasticsearch的哪些地方以及如何使用)  


Kibana是ELK Stack –日志分析解决方案的一部分。

它是一种开放源代码的可视化工具，可以以拖拽、自定义图表的方式直观分析数据，极大降低的数据分析的门槛。

未来会向类似：商业智能和分析软件 - Tableau 发展。


### [2、elasticsearch是如何实现master选举的](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#2elasticsearch是如何实现master选举的)  


`面试官`：想了解ES集群的底层原理，不再只关注业务层面了。

**前置前提：**

**1、** 只有候选主节点（master：true）的节点才能成为主节点。

**2、** 最小主节点数（min_master_nodes）的目的是防止脑裂。

这个我看了各种网上分析的版本和源码分析的书籍，云里雾里。

核对了一下代码，核心入口为findMaster，选择主节点成功返回对应Master，否则返回null。选举流程大致描述如下：

第一步：确认候选主节点数达标，elasticsearch.yml设置的值discovery.zen.minimum_master_nodes；

第二步：比较：先判定是否具备master资格，具备候选主节点资格的优先返回；若两节点都为候选主节点，则id小的值会主节点。注意这里的id为string类型。

题外话：获取节点id的方法。

```
 1GET /_cat/nodes?v&h=ip,port,heapPercent,heapMax,id,name
2ip        port heapPercent heapMax id   name
```


### [3、客户端在和集群连接时，是如何选择特定的节点执行请求的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#3客户端在和集群连接时是如何选择特定的节点执行请求的)  


TransportClient利用transport模块远程连接一个ElasticSearch集群。它并不加入到集群中，只是简单的获得一个或者多个初始化的transport地址，并以轮询的方式与这些地址进行通信。


### [4、你能告诉我 Elasticsearch 中的数据存储功能吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#4你能告诉我-elasticsearch-中的数据存储功能吗)  


Elasticsearch是一个搜索引擎，输入写入ES的过程就是索引化的过程，数据按照既定的 Mapping 序列化为Json 文档实现存储。


### [5、Master 节点和 候选 Master节点有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#5master-节点和-候选-master节点有什么区别)  


主节点负责集群相关的操作，例如创建或删除索引，跟踪哪些节点是集群的一部分，以及决定将哪些分片分配给哪些节点。

拥有稳定的主节点是衡量集群健康的重要标志。

而候选主节点是被选具备候选资格，可以被选为主节点的那些节点。


### [6、介绍下你们电商搜索的整体技术架构。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#6介绍下你们电商搜索的整体技术架构。)  


![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2019/08/0820/02/img_3.png#alt=img%5C_3.png)


### [7、客户端在和集群连接时，如何选择特定的节点执行请求的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#7客户端在和集群连接时如何选择特定的节点执行请求的)  


TransportClient 利用 transport 模块远程连接一个 elasticsearch 集群。它并不加入到集群中，只是简单的获得一个或者多个初始化的 transport 地址，并以 轮询 的方式与这些地址进行通信。


### [8、对于 GC 方面，在使用 Elasticsearch 时要注意什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#8对于-gc-方面在使用-elasticsearch-时要注意什么)  


**1、** SEE

**2、** 倒排词典的索引需要常驻内存，无法 GC，需要监控 data node 上 segmentmemory 增长趋势。

**3、** 各类缓存，field cache, filter cache, indexing cache, bulk queue 等等，要设置合理的大小，并且要应该根据最坏的情况来看 heap 是否够用，也就是各类缓存全部占满的时候，还有 heap 空间可以分配给其他任务吗？避免采用 clear cache等“自欺欺人”的方式来释放内存。

**4、** 避免返回大量结果集的搜索与聚合。确实需要大量拉取数据的场景，可以采用scan & scroll api 来实现。

**5、** cluster stats 驻留内存并无法水平扩展，超大规模集群可以考虑分拆成多个集群通过 tribe node 连接。

**6、** 想知道 heap 够不够，必须结合实际应用场景，并对集群的 heap 使用情况做持续的监控。


### [9、拼写纠错是如何实现的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#9拼写纠错是如何实现的)  


**1、拼写纠错是基于编辑距离来实现**；编辑距离是一种标准的方法，它用来表示经过插入、删除和替换操作从一个字符串转换到另外一个字符串的最小操作步数；

**2、编辑距离的计算过程：**比如要计算 batyu 和 beauty 的编辑距离，先创建一个7×8 的表（batyu 长度为 5，coffee 长度为 6，各加 2），接着，在如下位置填入

黑色数字。

**其他格的计算过程是取以下三个值的最小值：**

如果最上方的字符等于最左方的字符，则为左上方的数字。否则为左上方的数字 +1。（对于 3,3 来说为 0）左方数字+1（对于 3,3 格来说为 2）上方数字+1（对于 3,3 格来说为 2）

最终取右下角的值即为编辑距离的值 3。

![70_10.png][70_10.png]

对于拼写纠错，我们考虑构造一个度量空间（Metric Space），该空间内任何关

系满足以下三条基本条件：

> d(x,y) = 0 -- 假如 x 与 y 的距离为 0，则 x=y

d(x,y) = d(y,x) -- x 到 y 的距离等同于 y 到 x 的距离

d(x,y) + d(y,z) >= d(x,z) -- 三角不等式


**1、** 根据三角不等式，则满足与 query 距离在 n 范围内的另一个字符转 B，其与 A的距离最大为 d+n，最小为 d-n。

**2、** BK 树的构造就过程如下：每个节点有任意个子节点，每条边有个值表示编辑距离。所有子节点到父节点的边上标注 n 表示编辑距离恰好为 n。比如，我们有棵树父节点是”book”和两个子

**点”cake”和”books”，”book”到”books”的边标号 ：**

**1、** ”book”到”cake”的边上标号.

**2、** 从字典里构造好树后，无论何时你想插入新单词时.计算该单词与根节点的编辑距离，并且查找数值为 d(neweord, root)的边。递归得与各子节点进行比较，直到没有子节点，你就可以创建新的子节点并将新单词保存在那。比如，插入”boo”到刚才上述例子的树中，我们先检查根节点，查找 d(“book”, “boo”) = 1 的边，然后检查标号为1 的边的子节点，得到单词”books”。我们再计算距离 d(“books”, “boo”)=2，则将新单词插在”books”之后，边标号为 2。

**3、** 查询相似词如下：计算单词与根节点的编辑距离 d，然后递归查找每个子节点标号为 d-n 到 d+n（包含）的边。假如被检查的节点与搜索单词的距离 d 小于n，则返回该节点并继续查询。比如输入 cape 且最大容忍距离为 1，则先计算和根的编辑距离 d(“book”,“cape”)=4，然后接着找和根节点之间编辑距离为 3 到5 的，这个就找到了cake 这个节点，计算 d(“cake”, “cape”)=1，满足条件所以返回 cake，然后再找和 cake 节点编辑距离是 0 到 2 的，分别找到 cape 和cart 节点，这样就得到 cape 这个满足条件的结果。



### [10、在Elasticsearch中 cat API的功能是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题，2021年面试题及答案汇总.md#10在elasticsearch中-cat-api的功能是什么)  


cat API 命令提供了Elasticsearch 集群的分析、概述和运行状况，其中包括与别名，分配，索引，节点属性等有关的信息。

这些 cat 命令使用查询字符串作为其参数，并以J SON 文档格式返回结果信息。


### 11、在 Elasticsearch 中，是怎么根据一个词找到对应的倒排索引的？
### 12、ES更新数据的执行流程？
### 13、ElasticSearch是如何实现Master选举的？
### 14、ES在生产集群的部署架构是什么，每个索引有多大的数据量，每个索引有多少分片
### 15、elasticsearch 了解多少，说说你们公司 es 的集群架构，索引数据大小，分片有多少，以及一些调优手段 。
### 16、REST API在 Elasticsearch 方面有哪些优势？
### 17、请解释一下 Elasticsearch 中聚合？
### 18、什么是ElasticSearch索引？
### 19、ElasticSearch如何避免脑裂？
### 20、Elasticsearch 支持哪些配置管理工具？
### 21、详细描述一下 Elasticsearch 搜索的过程。
### 22、Elasticsearch中的节点（比如共20个），其中的10个选了一个master，另外10个选了另一个master，怎么办？
### 23、Elasticsearch中的属性 enabled, index 和 store 的功能是什么？
### 24、Elasticsearch 对于大数据量（上亿量级）的聚合如何实现？
### 25、如何监控Elasticsearch集群状态？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




