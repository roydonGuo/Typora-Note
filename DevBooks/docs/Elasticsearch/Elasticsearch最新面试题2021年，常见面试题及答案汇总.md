# Elasticsearch最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、我们可以在 Elasticsearch 中执行搜索的各种可能方式有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#1我们可以在-elasticsearch-中执行搜索的各种可能方式有哪些)  


核心方式如下：

方式一：基于 DSL 检索（最常用） Elasticsearch提供基于JSON的完整查询DSL来定义查询。

```
GET /shirts/_search
{
  "query": {
    "bool": {
      "filter": [
        { "term": { "color": "red"   }},
        { "term": { "brand": "gucci" }}
      ]
    }
  }
}
```

方式二：基于 URL 检索

```
GET /my_index/_search?q=user:seina
```

方式三：类SQL 检索

```
POST /_sql?format=txt
{
  "query": "SELECT * FROM uint-2020-08-17 ORDER BY itemid DESC LIMIT 5"
}
```

功能还不完备，不推荐使用。


### [2、ElasticSearch对于大数据量（上亿量级）的聚合如何实现？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#2elasticsearch对于大数据量上亿量级的聚合如何实现)  


ElasticSearch提供的首个近似聚合是cardinality度量。它提供一个字段的基数，即该字段的distinct或者unique值的数目。它是基于HLL算法的。HLL会先对我们的输入做哈希运算，然后根据哈希运算结果中的bits做概率估算从而得到基数。其特点是：

可配置的精度，用来控制内存的使用（更精确＝更多内存），小的数据集精度是非常高的；我们可以通过配置参数来设置去重需要的固定内存使用量，无论数千还是数十亿的唯一值，内存使用量只与你配置的精确度相关 。

图片


### [3、详细描述一下 Elasticsearch 索引文档的过程](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#3详细描述一下-elasticsearch-索引文档的过程)  


面试官：想了解 ES 的底层原理，不再只关注业务层面了。

解

这里的索引文档应该理解为文档写入 ES，创建索引的过程。文档写入包含：单文档写入和批量 bulk 写入，这里只解释一下：单文档写入流程。

**第一步：**客户写集群某节点写入数据，发送请求。（如果没有指定路由/协调节点，请求的节点扮演路由节点的角色。）

**第二步：**节点 1 接受到请求后，使用文档_id 来确定文档属于分片 0。请求会被转到另外的节点，假定节点 3。因此分片 0 的主分片分配到节点 3 上。

**第三步：**节点 3 在主分片上执行写操作，如果成功，则将请求并行转发到节点 1和节点 2 的副本分片上，等待结果返回。所有的副本分片都报告成功，节点 3 将向协调节点（节点 1）报告成功，节点 1 向请求客户端报告写入成功。

**如果面试官再问：**第二步中的文档获取分片的过程？

回借助路由算法获取，路由算法就是根据路由和文档 id 计算目标的分片 id 的

过程。

```
1shard = hash(_routing) % (num_of_primary_shards)
```


### [4、elasticsearch 数据预热](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#4elasticsearch-数据预热)  


数据预热是指，每隔一段时间，将热数据

手动在后台查询一遍，将热数据刷新到fileSystem cache上


### [5、如何使用 Elasticsearch Tokenizer？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#5如何使用-elasticsearch-tokenizer)  


Tokenizer 接收字符流（如果包含了字符过滤，则接收过滤后的字符流；否则，接收原始字符流），将其分词。同时记录分词后的顺序或位置(position)，以及开始值（start_offset）和偏移值(end_offset-start_offset)。


### [6、elasticsearch 数据的写入原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#6elasticsearch-数据的写入原理)  


es数据写入原理主要可以分为4个操作：

**1、** refresh

**2、** commit

**3、** flush

**4、** merge

| 操作触发条件 | 操作过程 |
| --- | --- |
| **refresh** | 1\\、每隔1s进行一次refresh操作
2\\、buffer已满，则进行一次refresh操作 |
| 2\\、清空buffer |  |
| **commit** | 1\\、每隔30分钟执行一次translog
2\\、translog日志已满 |
| 2\\、生成一个 commit point 文件标识此次操作一件把buffer数据执行到了哪一个segment文件
3\\、执行flush操作 |  |
| **flush** | commit操作中 |
| **merge** | 后台检查 |


![](https://image-static.segmentfault.com/284/854/2848546943-5e5b563ad0f06_articlex#alt=3chLse.png)


### [7、你是如何做 ElasticSearch 写入调优的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#7你是如何做-elasticsearch-写入调优的)  


1）写入前副本数设置为0；

2）写入前关闭refresh_interval设置为-1，禁用刷新机制；

3）写入过程中：采取bulk批量写入；

4） 写入后恢复副本数和刷新间隔；

5） 尽量使用自动生成的id。


### [8、Elasticsearch是如何实现Master选举的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#8elasticsearch是如何实现master选举的)  


**1、** Elasticsearch的选主是ZenDiscovery模块负责的，主要包含Ping（节点之间通过这个RPC来发现彼此）和Unicast（单播模块包含一个主机列表以控制哪些节点需要ping通）这两部分；

**2、** 对所有可以成为master的节点（**node.master: true**）根据nodeId字典排序，每次选举每个节点都把自己所知道节点排一次序，然后选出第一个（第0位）节点，暂且认为它是master节点。

**3、** 如果对某个节点的投票数达到一定的值（可以成为master节点数n/2+1）并且该节点自己也选举自己，那这个节点就是master。否则重新选举一直到满足上述条件。

**4、** 补充：master节点的职责主要包括集群、节点和索引的管理，不负责文档级别的管理；data节点可以关闭http功能*。


### [9、ElasticSearch主分片数量可以在后期更改吗？为什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#9elasticsearch主分片数量可以在后期更改吗为什么)  


不可以，因为根据路由算法shard = hash(document_id) % (num_of_primary_shards)，当主分片数量变化时会影响数据被路由到哪个分片上。


### [10、如何监控 Elasticsearch 集群状态？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Elasticsearch/Elasticsearch最新面试题2021年，常见面试题及答案汇总.md#10如何监控-elasticsearch-集群状态)  


Marvel 让你可以很简单的通过 Kibana 监控 Elasticsearch。你可以实时查看你的集群健康状态和性能，也可以分析过去的集群、索引和节点指标。


### 11、你能否在 Elasticsearch 中定义映射？
### 12、elasticsearch 的倒排索引是什么
### 13、lucence内部结构是什么？
### 14、详细描述一下ElasticSearch更新和删除文档的过程
### 15、在 Elasticsearch 中列出集群的所有索引的语法是什么？
### 16、elasticsearch 的 filesystem
### 17、Elasticsearch Analyzer 中的字符过滤器如何利用？
### 18、详细描述一下Elasticsearch搜索的过程。
### 19、什么是Elasticsearch Analyzer？
### 20、token filter 过滤器 在 Elasticsearch 中如何工作？
### 21、elasticsearch 数据的写入过程
### 22、迁移 Migration API 如何用作 Elasticsearch？
### 23、是否了解字典树？
### 24、详细说明ELK Stack及其内容？
### 25、ElasticSearch中的分析器是什么？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




