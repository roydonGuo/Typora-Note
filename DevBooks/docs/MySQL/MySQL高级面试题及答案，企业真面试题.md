# MySQL高级面试题及答案，企业真面试题


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是最左前缀原则？什么是最左匹配原则？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#1什么是最左前缀原则什么是最左匹配原则)  


最左前缀原则，就是最左优先，在创建多列索引时，要根据业务需求，where子句中使用最频繁的一列放在最左边。

当我们创建一个组合索引的时候，如(k1,k2,k3)，相当于创建了（k1）、(k1,k2)和(k1,k2,k3)三个索引，这就是最左匹配原则。。


### [2、myisamchk是用来做什么的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#2myisamchk是用来做什么的)  


它用来压缩MyISAM表，这减少了磁盘或内存使用。


### [3、4.说说分库与分表的设计](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#34说说分库与分表的设计)  


分库分表方案，分库分表中间件，分库分表可能遇到的问题

**「分库分表方案:」**

**1、** 水平分库：以字段为依据，按照一定策略（hash、range等），将一个库中的数据拆分到多个库中。

**2、** 水平分表：以字段为依据，按照一定策略（hash、range等），将一个表中的数据拆分到多个表中。

**3、** 垂直分库：以表为依据，按照业务归属不同，将不同的表拆分到不同的库中。

**4、** 垂直分表：以字段为依据，按照字段的活跃性，将表中字段拆到不同的表（主表和扩展表）中。

**「常用的分库分表中间件：」**

**1、** sharding-jdbc（当当）

**2、** Mycat

**3、** TDDL（淘宝）

**4、** Oceanus(58同城数据库中间件)

**5、** vitess（谷歌开发的数据库中间件）

**6、** Atlas(Qihoo 360)

**「分库分表可能遇到的问题」**

**1、** 事务问题：需要用分布式事务啦

**2、** 跨节点Join的问题：解决这一问题可以分两次查询实现

**3、** 跨节点的count,order by,group by以及聚合函数问题：分别在各个节点上得到结果后在应用程序端进行合并。

**4、** 数据迁移，容量规划，扩容等问题

**5、** ID问题：数据库被切分后，不能再依赖数据库自身的主键生成机制啦，最简单可以考虑UUID

**6、** 跨分片的排序分页问题（后台加大pagesize处理？）


### [4、什么情况下设置了索引但无法使用](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#4什么情况下设置了索引但无法使用)  


1.以“%”开头的LIKE语句，模糊匹配

2\、OR语句前后没有同时使用索引

3\、数据类型出现隐式转化（如varchar不加单引号的话可能会自动转换为int型）


### [5、如何删除索引](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#5如何删除索引)  


根据索引名删除普通索引、唯一索引、全文索引：`alter table 表名 drop KEY 索引名`

```
alter table user_index drop KEY name;
alter table user_index drop KEY id_card;
alter table user_index drop KEY information;
```

**删除主键索引：**`alter table 表名 drop primary key`（因为主键只有一个）。这里值得注意的是，如果主键自增长，那么不能直接执行此操作（自增长依赖于主键索引）：

![99_3.png][99_3.png]

**需要取消自增长再行删除：**

```
alter table user_index
-- 重新定义字段
MODIFY id int,
drop PRIMARY KEY
```

但通常不会删除主键，因为设计主键一定与业务逻辑无关。


### [6、什么是数据库连接池?为什么需要数据库连接池呢?](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#6什么是数据库连接池为什么需要数据库连接池呢)  


**连接池基本原理：**

数据库连接池原理：在内部对象池中，维护一定数量的数据库连接，并对外暴露数据库连接的获取和返回方法。

**应用程序和数据库建立连接的过程：**

**1、** 通过TCP协议的三次握手和数据库服务器建立连接

**2、** 发送数据库用户账号密码，等待数据库验证用户身份

**3、** 完成身份验证后，系统可以提交SQL语句到数据库执行

**4、** 把连接关闭，TCP四次挥手告别。

**数据库连接池好处：**

**1、** 资源重用 (连接复用)

**2、** 更快的系统响应速度

**3、** 新的资源分配手段

**4、** 统一的连接管理，避免数据库连接泄漏


### [7、列对比运算符是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#7列对比运算符是什么)  


在SELECT语句的列比较中使用=，<>，<=，<，> =，>，<<，>>，<=>，AND，OR或LIKE运算符。


### [8、按照锁的粒度分，数据库锁有哪些呢？锁机制与InnoDB锁算法](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#8按照锁的粒度分数据库锁有哪些呢锁机制与innodb锁算法)  


按锁粒度分有：表锁，页锁，行锁

按锁机制分有：乐观锁，悲观锁


### [9、LIKE声明中的％和_是什么意思？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#9like声明中的％和_是什么意思)  


％对应于0个或更多字符，_只是LIKE语句中的一个字符。

**如何在Unix和MySQL时间戳之间进行转换？**

UNIX_TIMESTAMP是从MySQL时间戳转换为Unix时间戳的命令

FROM_UNIXTIME是从Unix时间戳转换为MySQL时间戳的命令


### [10、如何定位及优化SQL语句的性能问题？创建的索引有没有被使用到?或者说怎么才可以知道这条语句运行很慢的原因？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题及答案，企业真面试题.md#10如何定位及优化sql语句的性能问题创建的索引有没有被使用到或者说怎么才可以知道这条语句运行很慢的原因)  


对于低性能的SQL语句的定位，最重要也是最有效的方法就是使用执行计划，MySQL提供了explain命令来查看语句的执行计划。 我们知道，不管是哪种数据库，或者是哪种数据库引擎，在对一条SQL语句进行执行的过程中都会做很多相关的优化，**对于查询语句，最重要的优化方式就是使用索引**。 而**执行计划，就是显示数据库引擎对于SQL语句的执行的详细情况，其中包含了是否使用索引，使用什么索引，使用的索引的相关信息等**。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/5/2/049/50/99_7.png#alt=99%5C_7.png)

执行计划包含的信息 **id** 有一组数字组成。表示一个查询中各个子查询的执行顺序;

**1、** id相同执行顺序由上至下。

**2、** id不同，id值越大优先级越高，越先被执行。

**3、** id为null时表示一个结果集，不需要使用它查询，常出现在包含union等查询语句中。

**select_type** 每个子查询的查询类型，一些常见的查询类型。

| id | select_type | description |
| --- | --- | --- |
| 1 | SIMPLE | 不包含任何子查询或union等查询 |
| 2 | PRIMARY | 包含子查询最外层查询就显示为 PRIMARY |
| 3 | SUBQUERY | 在select或 where字句中包含的查询 |
| 4 | DERIVED | from字句中包含的查询 |
| 5 | UNION | 出现在union后的查询语句中 |
| 6 | UNION RESULT | 从UNION中获取结果集，例如上文的第三个例子 |


**table** 查询的数据表，当从衍生表中查数据时会显示 x 表示对应的执行计划id **partitions** 表分区、表创建的时候可以指定通过那个列进行表分区。 举个例子：

```
create table tmp (
id int unsigned not null AUTO_INCREMENT,
name varchar(255),
PRIMARY KEY (id)
) engine = innodb
partition by key (id) partitions 5;
```

**type**(非常重要，可以看到有没有走索引) 访问类型

**1、** ALL 扫描全表数据

**2、** index 遍历索引

**3、** range 索引范围查找

**4、** index_subquery 在子查询中使用 ref

**5、** unique_subquery 在子查询中使用 eq_ref

**6、** ref_or_null 对Null进行索引的优化的 ref

**7、** fulltext 使用全文索引

**8、** ref 使用非唯一索引查找数据

**9、** eq_ref 在join查询中使用PRIMARY KEYorUNIQUE NOT NULL索引关联。

**10、**  **possible_keys** 可能使用的索引，注意不一定会使用。查询涉及到的字段上若存在索引，则该索引将被列出来。当该列为 NULL时就要考虑当前的SQL是否需要优化了。

**11、**  **key** 显示MySQL在查询中实际使用的索引，若没有使用索引，显示为NULL。

**12、**  **TIPS**:查询中若使用了覆盖索引(覆盖索引：索引的数据覆盖了需要查询的所有数据)，则该索引仅出现在key列表中

**13、**  **key_length** 索引长度

**14、**  **ref** 表示上述表的连接匹配条件，即哪些列或常量被用于查找索引列上的值

**15、**  **rows** 返回估算的结果集数目，并不是一个准确的值。

**16、**  **extra** 的信息非常丰富，常见的有：

**17、** Using index 使用覆盖索引

**18、** Using where 使用了用where子句来过滤结果集

**19、** Using filesort 使用文件排序，使用非索引列进行排序时出现，非常消耗性能，尽量优化。

**20、** Using temporary 使用了临时表 sql优化的目标可以参考阿里开发手册

**推荐**

SQL性能优化的目标：至少要达到 range 级别，要求是ref级别，如果可以是consts最好

**说明：**

**1、** consts 单表中最多只有一个匹配行（主键或者唯一索引），在优化阶段即可读取到数据。

**2、** ref 指的是使用普通的索引（normal index）。

**3、** range 对索引进行范围检索。

**反例：**

explain表的结果，type=index，索引物理文件全扫描，速度非常慢，这个index级别比较range还低，与全表扫描是小巫见大巫。


### 11、MySQL 的内连接、左连接、右连接有什么区别？
### 12、索引的基本原理
### 13、varchar(50)中50的涵义
### 14、MySql, Oracle，Sql Service的区别
### 15、什么是通用SQL函数？
### 16、创建索引有什么原则呢？
### 17、MySQL的复制原理以及流程
### 18、你是如何监控你们的数据库的？你们的慢日志都是怎么查询的？
### 19、简述在MySQL数据库中MyISAM和InnoDB的区别
### 20、日志的存放形式
### 21、创建索引的原则？
### 22、Blob和text有什么区别？
### 23、主从同步延迟的原因
### 24、说说分库与分表的设计
### 25、MYSQL支持事务吗？
### 26、MySQL有关权限的表都有哪几个
### 27、什么是触发器？触发器的使用场景有哪些？
### 28、简述有哪些索引和作用
### 29、数据库中的事务是什么?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




