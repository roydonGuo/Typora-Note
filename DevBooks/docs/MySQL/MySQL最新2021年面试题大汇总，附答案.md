# MySQL最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、innoDB的B+Tree 存储整行数据和主键的值得区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#1innodb的b+tree-存储整行数据和主键的值得区别)  


**1、** 整行数据：innoDB的B+Tree存储了整行数据的是主键索引，也被成为聚凑索引。

**2、** 存储主键的值：成为非主键索引，也被称为非聚凑索引


### [2、读写分离常见方案？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#2读写分离常见方案)  


**1、** 应用程序根据业务逻辑来判断，增删改等写操作命令发给主库，查询命令发给备库。

**2、** 利用中间件来做代理，负责对数据库的请求识别出读还是写，并分发到不同的数据库中。（如：amoeba，MySQL-proxy）


### [3、六种关联查询](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#3六种关联查询)  


**1、** 交叉连接（CROSS JOIN）

**2、** 内连接（INNER JOIN）

**3、** 外连接（LEFT JOIN/RIGHT JOIN）

**4、** 联合查询（UNION与UNION ALL）

**5、** 全连接（FULL JOIN）

**6、** 交叉连接（CROSS JOIN）

```
SELECT * FROM A,B(,C)或者SELECT * FROM A CROSS JOIN B (CROSS JOIN C)#没有任何关联条件，结果是笛卡尔积，结果集会很大，没有意义，很少使用内连接（INNER JOIN）SELECT * FROM A,B WHERE A.id=B.id或者SELECT * FROM A INNER JOIN B ON A.id=B.id多表中同时符合某种条件的数据记录的集合，INNER JOIN可以缩写为JOIN
```

**内连接分为三类**

**1、** 等值连接：ON A.id=B.id

**2、** 不等值连接：ON A.id > B.id

**3、** 自连接：SELECT * FROM A T1 INNER JOIN A T2 ON T1.id=T2.pid

**外连接（LEFT JOIN/RIGHT JOIN）**

**左外连接：**

LEFT OUTER JOIN, 以左表为主，先查询出左表，按照ON后的关联条件匹配右表，没有匹配到的用NULL填充，可以简写成LEFT JOIN

**右外连接：**

RIGHT OUTER JOIN, 以右表为主，先查询出右表，按照ON后的关联条件匹配左表，没有匹配到的用NULL填充，可以简写成RIGHT JOIN

**联合查询（UNION与UNION ALL）**

```
SELECT * FROM A UNION SELECT * FROM B UNION ...
```

**1、** 就是把多个结果集集中在一起，UNION前的结果为基准，需要注意的是联合查询的列数要相等，相同的记录行会合并

**2、** 如果使用UNION ALL，不会合并重复的记录行

**3、** 效率 UNION 高于 UNION ALL

**全连接（FULL JOIN）**

```
SELECT * FROM A LEFT JOIN B ON A.id=B.id UNIONSELECT * FROM A RIGHT JOIN B ON A.id=B.id
```

MySQL不支持全连接

可以使用LEFT JOIN 和UNION和RIGHT JOIN联合使用

**有2张表**

1张R、1张S，R表有ABC三列，S表有CD两列，表中各有三条记录

**R表**

| A | B | C |
| --- | --- | --- |
| a1 | b1 | c1 |
| a2 | b2 | c2 |
| a3 | b3 | c3 |


**S表**

| C | D |
| --- | --- |
| c1 | d1 |
| c2 | d2 |
| c4 | d3 |


**交叉连接(笛卡尔积)**

SQL

```
select r.*,s.* from r,s
```

**结果**

| A | B | C | C | D |
| --- | --- | --- | --- | --- |
| a1 | b1 | c1 | c1 | d1 |
| a2 | b2 | c2 | c1 | d1 |
| a3 | b3 | c3 | c1 | d1 |
| a1 | b1 | c1 | c2 | d2 |
| a2 | b2 | c2 | c2 | d2 |
| a3 | b3 | c3 | c2 | d2 |
| a1 | b1 | c1 | c4 | d3 |
| a2 | b2 | c2 | c4 | d3 |
| a3 | b3 | c3 | c4 | d3 |


**内连接结果**

SQL

```
select r.*,s.* from r inner join s on r.c=s.c
```

**结果**

| A | B | C | C | D |
| --- | --- | --- | --- | --- |
| a1 | b1 | c1 | c1 | d1 |
| a2 | b2 | c2 | c2 | d2 |


**左连接结果**

SQL

```
select r.*,s.* from r left join s on r.c=s.c
```

**结果**

| A | B | C | C | D |
| --- | --- | --- | --- | --- |
| a1 | b1 | c1 | c1 | d1 |
| a2 | b2 | c2 | c2 | d2 |
| a3 | b3 | c3 |  |  |


**右连接结果**

SQL

```
select r.*,s.* from r right join s on r.c=s.c
```

**结果**

| A | B | C | C | D |
| --- | --- | --- | --- | --- |
| a1 | b1 | c1 | c1 | d1 |
| a2 | b2 | c2 | c2 | d2 |
|  |  |  | c4 | d3 |


**全表连接的结果（MySql不支持，Oracle支持）**

SQL

```
select r.*,s.* from r full join s on r.c=s.c
```

**结果**

| A | B | C | C | D |
| --- | --- | --- | --- | --- |
| a1 | b1 | c1 | c1 | d1 |
| a2 | b2 | c2 | c2 | d2 |
| a3 | b3 | c3 |  |  |
|  |  |  | c4 | d3 |



### [4、什么是存储过程？有哪些优缺点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#4什么是存储过程有哪些优缺点)  


**存储过程**，就是一些编译好了的SQL语句，这些SQL语句代码像一个方法一样实现一些功能（对单表或多表的增删改查），然后给这些代码块取一个名字，在用到这个功能的时候调用即可。

**优点：**

**1、** 存储过程是一个预编译的代码块，执行效率比较高

**2、** 存储过程在服务器端运行，减少客户端的压力

**3、** 允许模块化程序设计，只需要创建一次过程，以后在程序中就可以调用该过程任意次，类似方法的复用

**4、** 一个存储过程替代大量T_SQL语句 ，可以降低网络通信量，提高通信速率

**5、** 可以一定程度上确保数据安全

**缺点：**

**1、** 调试麻烦

**2、** 可移植性不灵活

**3、** 重新编译问题


### [5、优化关联查询](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#5优化关联查询)  


**1、** 确定ON或者USING子句中是否有索引。

**2、** 确保GROUP BY和ORDER BY只有一个表中的列，这样MySQL才有可能使用索引。


### [6、主键和候选键有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#6主键和候选键有什么区别)  


表格的每一行都由主键唯一标识,一个表只有一个主键。

主键也是候选键。按照惯例，候选键可以被指定为主键，并且可以用于任何外键引用。


### [7、既然提到了InnoDB使用户的B+树的索引模型](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#7既然提到了innodb使用户的b+树的索引模型)  


**那么你知道为什么采用B+树吗？这和Hash索引比较起来有什么缺点吗？**

因为hash索引底层是哈希表，哈希表是一种以key-value存储数据的结构，所以多个数据在存储关系上是完全没有任何顺序关系的，所以，对于区间查询是无法直接通过索引查询的，就需要全表扫描。所以，哈希索引只适用于等值查询的场景。而B+树是一种多路平衡查询树，所以他的节点是天然有序的（左子节点小于父节点，父节点小于右子节点），所以对于范围查询的时候不需要做全表扫描。


### [8、MySQL_fetch_array和MySQL_fetch_object的区别是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#8mysql_fetch_array和mysql_fetch_object的区别是什么)  


以下是MySQL_fetch_array和MySQL_fetch_object的区别：

MySQL_fetch_array（） – 将结果行作为关联数组或来自数据库的常规数组返回。

MySQL_fetch_object – 从数据库返回结果行作为对象。


### [9、对于关系型数据库而言，索引是相当重要的概念，请回答有关索引的几个问题：](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#9对于关系型数据库而言索引是相当重要的概念请回答有关索引的几个问题：)  


**1、** 索引的目的是什么？

快速访问数据表中的特定信息，提高检索速度

创建唯一性索引，保证数据库表中每一行数据的唯一性。

加速表和表之间的连接

使用分组和排序子句进行数据检索时，可以显著减少查询中分组和排序的时间

**2、** 索引对数据库系统的负面影响是什么？

负面影响：

创建索引和维护索引需要耗费时间，这个时间随着数据量的增加而增加；索引需要占用物理空间，不光是表需要占用数据空间，每个索引也需要占用物理空间；当对表进行增、删、改、的时候索引也要动态维护，这样就降低了数据的维护速度。

**3、** 为数据表建立索引的原则有哪些？

在最频繁使用的、用以缩小查询范围的字段上建立索引。

在频繁使用的、需要排序的字段上建立索引

**4、** 什么情况下不宜建立索引？

对于查询中很少涉及的列或者重复值比较多的列，不宜建立索引。

对于一些特殊的数据类型，不宜建立索引，比如文本字段（text）等


### [10、MySQL如何优化DISTINCT？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题大汇总，附答案.md#10mysql如何优化distinct)  


DISTINCT在所有列上转换为GROUP BY，并与ORDER BY子句结合使用。

1

SELECT DISTINCT t1.a FROM t1,t2 where t1.a=t2.a;


### 11、什么是幻读，脏读，不可重复读呢？
### 12、linux添加索引
### 13、B+树在满足聚簇索引和覆盖索引的时候不需要回表查询数据？
### 14、数据库中间件了解过吗，sharding jdbc，mycat？
### 15、为什么要使用视图？什么是视图？
### 16、NULL是什么意思
### 17、MySQL中InnoDB引擎的行锁是怎么实现的？
### 18、优化器的执行过程？
### 19、什么是最左前缀原则？什么是最左匹配原则
### 20、LIKE声明中的％和_是什么意思？
### 21、使用乐观锁
### 22、varchar(50)中50的涵义
### 23、主从同步延迟的解决办法
### 24、MySQL 遇到过死锁问题吗，你是如何解决的？
### 25、主键使用自增ID还是UUID，为什么？
### 26、什么是数据库事务？
### 27、怎么查询SQL语句是否使用了索引查询？
### 28、什么是死锁？怎么解决？
### 29、主键使用自增ID还是UUID？
### 30、MVCC熟悉吗，它的底层原理？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




