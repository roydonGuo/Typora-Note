# MySQL最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、一个6亿的表a，一个3亿的表b，通过外间tid关联，你如何最快的查询出满足条件的第50000到第50200中的这200条数据记录。](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#1一个6亿的表a一个3亿的表b通过外间tid关联你如何最快的查询出满足条件的第50000到第50200中的这200条数据记录。)  


**1、** 如果A表TID是自增长,并且是连续的,B表的ID为索引 select * from a,b where a.tid = b.id and a.tid>500000 limit 200;

**2、** 如果A表的TID不是连续的,那么就需要使用覆盖索引.TID要么是主键,要么是辅助索引,B表ID也需要有索引。 select * from b , (select tid from a limit 50000,200) a where b.id = a .tid;


### [2、SQL语句优化的一些方法](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#2sql语句优化的一些方法)  


**1、** 对查询进行优化，应尽量避免全表扫描，首先应考虑在 where 及 order by 涉及的列上建立索引。

**2、** 应尽量避免在 where 子句中对字段进行 null 值判断，否则将导致引擎放弃使用索引而进行全表扫描，如：

```
select id from t where num is null
-- 可以在num上设置默认值0，确保表中num列没有null值，然后这样查询：
select id from t where num=0
```

**3、** 应尽量避免在 where 子句中使用!=或<>操作符，否则引擎将放弃使用索引而进行全表扫描。

**4、** 应尽量避免在 where 子句中使用or 来连接条件，否则将导致引擎放弃使用索引而进行全表扫描，如：

```
select id from t where num=10 or num=20
-- 可以这样查询：
select id from t where num=10 union all select id from t where num=20
```

5、in 和 not in 也要慎用，否则会导致全表扫描，如：

```
select id from t where num in(1,2,3) 
-- 对于连续的数值，能用 between 就不要用 in 了：
select id from t where num between 1 and 3
```

**6、** 下面的查询也将导致全表扫描：select id from t where name like ‘%李%’若要提高效率，可以考虑全文检索。

**7、** 如果在 where 子句中使用参数，也会导致全表扫描。因为SQL只有在运行时才会解析局部变量，但优化程序不能将访问计划的选择推迟到运行时；它必须在编译时进行选择。然 而，如果在编译时建立访问计划，变量的值还是未知的，因而无法作为索引选择的输入项。如下面语句将进行全表扫描：

```
select id from t where num=@num
-- 可以改为强制查询使用索引：
select id from t with(index(索引名)) where num=@num
```

**8、** 应尽量避免在 where 子句中对字段进行表达式操作，这将导致引擎放弃使用索引而进行全表扫描。如：

```
select id from t where num/2=100
-- 应改为:
select id from t where num=100*2
```

**9、** 应尽量避免在where子句中对字段进行函数操作，这将导致引擎放弃使用索引而进行全表扫描。如：

```
select id from t where substring(name,1,3)=’abc’
-- name以abc开头的id应改为:
select id from t where name like ‘abc%’
```

**10、** 不要在 where 子句中的“=”左边进行函数、算术运算或其他表达式运算，否则系统将可能无法正确使用索引。


### [3、什么是数据库连接池?为什么需要数据库连接池呢?](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#3什么是数据库连接池为什么需要数据库连接池呢)  


「连接池基本原理：」 数据库连接池原理：在内部对象池中，维护一定数量的数据库连接，并对外暴露数据库连接的获取和返回方法。

**「应用程序和数据库建立连接的过程：」**

**1、** 通过TCP协议的三次握手和数据库服务器建立连接

**2、** 发送数据库用户账号密码，等待数据库验证用户身份

**3、** 完成身份验证后，系统可以提交SQL语句到数据库执行

**4、** 把连接关闭，TCP四次挥手告别。

**「数据库连接池好处：」**

**1、** 资源重用 (连接复用)

**2、** 更快的系统响应速度

**3、** 新的资源分配手段

**4、** 统一的连接管理，避免数据库连接泄漏


### [4、事物的四大特性(ACID)介绍一下?](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#4事物的四大特性acid介绍一下)  


关系性数据库需要遵循ACID规则，具体内容如下：

![99_6.png][99_6.png]

**1、** 原子性：

事务是最小的执行单位，不允许分割。事务的原子性确保动作要么全部完成，要么完全不起作用；

**2、** 一致性：

执行事务前后，数据保持一致，多个事务对同一个数据读取的结果是相同的；

**3、** 隔离性：

并发访问数据库时，一个用户的事务不被其他事务所干扰，各并发事务之间数据库是独立的；

**4、** 持久性：

一个事务被提交之后。它对数据库中数据的改变是持久的，即使数据库发生故障也不应该对其有任何影响。


### [5、索引分类？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#5索引分类)  


**单列索引**

**1、** 普通索引：MySQL中基本索引类型，没有什么限制，允许在定义索引的列中插入重复值和空值，纯粹为了查询数据更快一点。

**2、** 唯一索引：索引列中的值必须是唯一的，但是允许为空值，

**3、** 主键索引：是一种特殊的唯一索引，不允许有空值。

**组合索引：**

多个字段组合上创建的索引，只有在查询条件中使用了这些字段的左边字段时，索引才会被使用，使用组合索引时遵循最左前缀集合。

**全文索引：**

只有在MyISAM引擎上才能使用，只能在CHAR,VARCHAR,TEXT    类型字段上使用全文索引，介绍了要求，说说什么是全文索引，就是在一堆文字中，通过其中的某个关键字等，就能找到该字段所属的记录行，比如有"你是个靓仔，靓女 ..."   通过靓仔，可能就可以找到该条记录

**空间索引：**

空间索引是对空间数据类型的字段建立的索引，MySQL中的空间数据类型有四种，GEOMETRY、POINT、LINESTRING、POLYGON。在创建空间索引时，使用SPATIAL关键字。要求，引擎为MyISAM，创建空间索引的列，必须将其声明为NOT NULL。


### [6、锁的优化策略](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#6锁的优化策略)  


1\、读写分离

2\、分段加锁

3\、减少锁持有的时间

4\、多个线程尽量以相同的顺序去获取资源

不能将锁的粒度过于细化，不然可能会出现线程的加锁和释放次数过多，反而效率不如一次加一把大锁。


### [7、limit 1000000 加载很慢的话，你是怎么解决的呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#7limit-1000000-加载很慢的话你是怎么解决的呢)  


**方案一：如果id是连续的，可以这样，返回上次查询的最大记录(偏移量)，再往下limit**

```
select id，name from employee where id>1000000 limit 10.
```

**方案二：在业务允许的情况下限制页数：**

建议跟业务讨论，有没有必要查这么后的分页啦。因为绝大多数用户都不会往后翻太多页。

**方案三：order by + 索引（id为索引）**

```
select id，name from employee order by id  limit 1000000，10
```

**方案四：利用延迟关联或者子查询优化超多分页场景。（先快速定位需要获取的id段，然后再关联）**

```
SELECT a.* FROM employee a, (select id from employee where 条件 LIMIT 1000000,10 ) b where a.id=b.id
```


### [8、什么是事务的隔离级别？MySQL的默认隔离级别是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#8什么是事务的隔离级别mysql的默认隔离级别是什么)  


为了达到事务的四大特性，数据库定义了4种不同的事务隔离级别，由低到高依次为Read uncommitted、Read committed、Repeatable read、Serializable，这四个级别可以逐个解决脏读、不可重复读、幻读这几类问题。

| 隔离级别 | 脏读 | 不可重复读 | 幻影读 |
| --- | --- | --- | --- |
| READ-UNCOMMITTED | √ | √ | √ |
| READ-COMMITTED | × | √ | √ |
| REPEATABLE-READ | × | × | √ |
| SERIALIZABLE |  |  |  |


**SQL 标准定义了四个隔离级别：**

**1、** READ-UNCOMMITTED(读取未提交)：

最低的隔离级别，允许读取尚未提交的数据变更，**可能会导致脏读、幻读或不可重复读**。

**2、** READ-COMMITTED(读取已提交)： 允许读取并发事务已经提交的数据，**可以阻止脏读，但是幻读或不可重复读仍有可能发生**。

**3、** REPEATABLE-READ(可重复读)：

对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，**可以阻止脏读和不可重复读，但幻读仍有可能发生**。

**4、** SERIALIZABLE(可串行化)：

最高的隔离级别，完全服从ACID的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，**该级别可以防止脏读、不可重复读以及幻读**。

**注意：**

**1、** 这里需要注意的是：MySQL 默认采用的 REPEATABLE_READ隔离级别 Oracle 默认采用的 READ_COMMITTED隔离级别

**2、** 事务隔离机制的实现基于锁机制和并发调度。其中并发调度使用的是MVVC（多版本并发控制），通过保存修改的旧版本信息来支持并发一致性读和回滚等特性。

**3、** 因为隔离级别越低，事务请求的锁越少，所以大部分数据库系统的隔离级别都是**READ-COMMITTED(读取提交内容):**，但是你要知道的是InnoDB 存储引擎默认使用 **REPEATABLE-READ（可重读）**并不会有任何性能损失。

**4、** InnoDB 存储引擎在 **分布式事务** 的情况下一般会用到**SERIALIZABLE(可串行化)**隔离级别。


### [9、视图的使用场景有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#9视图的使用场景有哪些)  


视图根本用途：简化sql查询，提高开发效率。如果说还有另外一个用途那就是兼容老的表结构

**下面是视图的常见使用场景：**

**1、** 重用SQL语句；

**2、** 简化复杂的SQL操作。在编写查询后，可以方便的重用它而不必知道它的基本查询细节；

**3、** 使用表的组成部分而不是整个表；

**4、** 保护数据。可以给用户授予表的特定部分的访问权限而不是整个表的访问权限；

**5、** 更改数据格式和表示。视图可返回与底层表的表示和格式不同的数据。


### [10、MYSQL数据库服务器性能分析的方法命令有哪些?](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL最新2021年面试题，高级面试题及附答案解析.md#10mysql数据库服务器性能分析的方法命令有哪些)  


Show status, 一些值得监控的变量值：

**1、** Bytes_received和Bytes_sent 和服务器之间来往的流量。

**2、** Com_*服务器正在执行的命令。

**3、** Created_*在查询执行期限间创建的临时表和文件。

**4、** Handler_*存储引擎操作。

**5、** Select_*不同类型的联接执行计划。

**6、** Sort_*几种排序信息。

Show profiles 是MySql用来分析当前会话SQL语句执行的资源消耗情况


### 11、列值为NULL时，查询是否会用到索引？
### 12、MySQL里记录货币用什么字段类型好
### 13、在高并发情况下，如何做到安全的修改同一行数据？
### 14、B+树在满足聚簇索引和覆盖索引的时候不需要回表查询数据，
### 15、SQL语言包括哪几部分？每部分都有哪些操作关键字？
### 16、优化特定类型的查询语句
### 17、什么是数据库事务？
### 18、谈谈MySQL的Explain
### 19、视图的优点，缺点，讲一下？
### 20、MyISAM Static和MyISAM Dynamic有什么区别？
### 21、隔离级别与锁的关系
### 22、如何优化长难的查询语句？有实战过吗？
### 23、B+Tree的页子节点都可以存放哪些东西？
### 24、SQL语句的语法顺序：
### 25、什么是锁？
### 26、你怎么看到为表格定义的所有索引？
### 27、MySQL里记录货币用什么字段类型比较好？
### 28、数据库的乐观锁和悲观锁。
### 29、MySQL有关权限的表都有哪几个？
### 30、索引不适合哪些场景





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




