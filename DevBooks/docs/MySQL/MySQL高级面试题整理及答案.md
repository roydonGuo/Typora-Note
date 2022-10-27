# MySQL高级面试题整理及答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、索引的分类?](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#1索引的分类)  


**1、** 从存储结构上来划分：BTree索引（B-Tree或B+Tree索引），Hash索引，full-index全文索引，R-Tree索引。这里所描述的是索引存储时保存的形式，

**2、** 从应用层次来分：普通索引，唯一索引，复合索引

**3、** 根据中数据的物理顺序与键值的逻辑（索引）顺序关系：聚集索引，非聚集索引。

平时讲的索引类型一般是指在应用层次的划分。

就像手机分类：安卓手机，IOS手机 与 华为手机，苹果手机，OPPO手机一样。

普通索引：

即一个索引只包含单个列，一个表可以有多个单列索引

唯一索引：

索引列的值必须唯一，但允许有空值

复合索引：

多列值组成一个索引，专门用于组合搜索，其效率大于索引合并

聚簇索引(聚集索引)：

并不是一种单独的索引类型，而是一种数据存储方式。具体细节取决于不同的实现，InnoDB的聚簇索引其实就是在同一个结构中保存了B-Tree索引(技术上来说是B+Tree)和数据行。

非聚簇索引：不是聚簇索引，就是非聚簇索引


### [2、索引具体采用那种数据结构呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#2索引具体采用那种数据结构呢)  


常见的MySQL主要有两种结构：hash索引和B+Tree索引，我们使用的是innodb引擎，默认的是B+树。


### [3、索引算法有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#3索引算法有哪些)  


索引算法有 BTree算法和Hash算法

**BTree算法**

BTree是最常用的MySQL数据库索引算法，也是MySQL默认的算法。因为它不仅可以被用在=,>,>=,<,<=和between这些比较操作符上，而且还可以用于like操作符，只要它的查询条件是一个不以通配符开头的常量， 例如：

```
-- 只要它的查询条件是一个不以通配符开头的常量
select * from user where name like 'jack%'; 
-- 如果一通配符开头，或者没有使用常量，则不会使用索引，例如： 
select * from user where name like '%jack';
```

**Hash算法**

Hash Hash索引只能用于对等比较，例如=,<=>（相当于=）操作符。由于是一次定位数据，不像BTree索引需要从根节点到枝节点，最后才能访问到页节点这样多次IO访问，所以检索效率远高于BTree索引。


### [4、备份计划，MySQLdump以及xtranbackup的实现原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#4备份计划mysqldump以及xtranbackup的实现原理)  


**备份计划**

**1、** 视库的大小来定，一般来说 100G 内的库，可以考虑使用 MySQLdump 来做，因为 MySQLdump更加轻巧灵活，备份时间选在业务低峰期，可以每天进行都进行全量备份(MySQLdump 备份出来的文件比较小，压缩之后更小)。

**2、** 100G 以上的库，可以考虑用 xtranbackup 来做，备份速度明显要比 MySQLdump 要快。一般是选择一周一个全备，其余每天进行增量备份，备份时间为业务低峰期。

**备份恢复时间**

**1、** 物理备份恢复快，逻辑备份恢复慢

**2、** 这里跟机器，尤其是硬盘的速率有关系，以下列举几个仅供参考

**3、** 20G的2分钟（MySQLdump）

**4、** 80G的30分钟(MySQLdump)

**5、** 111G的30分钟（MySQLdump)

**6、** 288G的3小时（xtra)

**7、** 3T的4小时（xtra)

**8、** 逻辑导入时间一般是备份时间的5倍以上

**备份恢复失败如何处理**

首先在恢复之前就应该做足准备工作，避免恢复的时候出错。比如说备份之后的有效性检查、权限检查、空间检查等。如果万一报错，再根据报错的提示来进行相应的调整。

**MySQLdump和xtrabackup实现原理**

**MySQLdump**

MySQLdump 属于逻辑备份。加入–single-transaction 选项可以进行一致性备份。后台进程会先设置 session 的事务隔离级别为 RR(SET SESSION TRANSACTION ISOLATION LEVELREPEATABLE READ)，之后显式开启一个事务(START TRANSACTION /*!40100 WITH CONSISTENTSNAPSHOT */)，这样就保证了该事务里读到的数据都是事务事务时候的快照。之后再把表的数据读取出来。如果加上–master-data=1 的话，在刚开始的时候还会加一个数据库的读锁(FLUSH TABLES WITH READ LOCK),等开启事务后，再记录下数据库此时 binlog 的位置(showmaster status)，马上解锁，再读取表的数据。等所有的数据都已经导完，就可以结束事务

**Xtrabackup:**

xtrabackup 属于物理备份，直接拷贝表空间文件，同时不断扫描产生的 redo 日志并保存下来。最后完成 innodb 的备份后，会做一个 flush engine logs 的操作(老版本在有 bug，在5.6 上不做此操作会丢数据)，确保所有的 redo log 都已经落盘(涉及到事务的两阶段提交

- 概念，因为 xtrabackup 并不拷贝 binlog，所以必须保证所有的 redo log 都落盘，否则可能会丢最后一组提交事务的数据)。这个时间点就是 innodb 完成备份的时间点，数据文件虽然不是一致性的，但是有这段时间的 redo 就可以让数据文件达到一致性(恢复的时候做的事情)。然后还需要 flush tables with read lock，把 myisam 等其他引擎的表给备份出来，备份完后解锁。这样就做到了完美的热备。


### [5、BLOB和TEXT有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#5blob和text有什么区别)  


BLOB是一个二进制对象，可以容纳可变数量的数据。TEXT是一个不区分大小写的BLOB。

BLOB和TEXT类型之间的唯一区别在于对BLOB值进行排序和比较时区分大小写，对TEXT值不区分大小写。


### [6、百万级别或以上的数据如何删除](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#6百万级别或以上的数据如何删除)  


关于索引：由于索引需要额外的维护成本，因为索引文件是单独存在的文件,所以当我们对数据的增加,修改,删除,都会产生额外的对索引文件的操作,这些操作需要消耗额外的IO,会降低增/改/删的执行效率。所以，在我们删除数据库百万级别数据的时候，查询MySQL官方手册得知删除数据的速度和创建的索引数量是成正比的。

**1、** 所以我们想要删除百万数据的时候可以先删除索引（此时大概耗时三分多钟）

**2、** 然后删除其中无用数据（此过程需要不到两分钟）

**3、** 删除完成后重新创建索引(此时数据较少了)创建索引也非常快，约十分钟左右。

**4、** 与之前的直接删除绝对是要快速很多，更别说万一删除中断,一切删除会回滚。那更是坑了。


### [7、乐观锁：](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#7乐观锁：)  


乐观锁的“乐观情绪”体现在，它认为数据的变动不会太频繁。因此，它允许多个事务同时对数据进行变动。实现方式：乐观锁一般会使用版本号机制或CAS算法实现。


### [8、B树和B+树的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#8b树和b+树的区别)  


**1、** 在B树中，你可以将键和值存放在内部节点和叶子节点；但在B+树中，内部节点都是键，没有值，叶子节点同时存放键和值。

**2、** B+树的叶子节点有一条链相连，而B树的叶子节点各自独立。

![99_4.png][99_4.png]


### [9、InnoDB引擎的4大特性](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#9innodb引擎的4大特性)  


**1、** 插入缓冲（insert buffer)

**2、** 二次写(double write)

**3、** 自适应哈希索引(ahi)

**4、** 预读(read ahead)


### [10、有多少种日志](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题整理及答案.md#10有多少种日志)  


innodb两种日志redo和undo。


### 11、MySQL的binlog有几种录入格式？分别有什么区别？
### 12、优化WHERE子句
### 13、什么是内连接、外连接、交叉连接、笛卡尔积呢？
### 14、聚簇索引和非聚簇索引，在查询数据的时候有区别吗？为什么？
### 15、SQL 约束有哪几种？
### 16、MySQL中有哪些不同的表格？
### 17、索引使用场景
### 18、MySQL为什么这么设计
### 19、drop、delete与truncate的区别
### 20、MySQL中TEXT数据类型的最大长度
### 21、CHAR和VARCHAR的区别？
### 22、怎么创建索引的，有什么好处，有哪些分类
### 23、MySQL中有哪几种锁？
### 24、你怎么知道SQL语句性能是高还是低
### 25、InnoDB引擎的4大特性，了解过吗
### 26、如何写sql能够有效的使用到复合索引。
### 27、使用悲观锁
### 28、Myql中的事务回滚机制概述
### 29、说说MySQL 的基础架构图





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




