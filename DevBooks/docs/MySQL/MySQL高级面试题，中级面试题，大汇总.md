# MySQL高级面试题，中级面试题，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、int(20)中20的涵义](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#1int20中20的涵义)  


**1、** 是指显示字符的长度。20表示最大显示宽度为20，但仍占4字节存储，存储范围不变；

**2、** 不影响内部存储，只是影响带 zerofill 定义的 int 时，前面补多少个 0，易于报表展示


### [2、为什么索引结构默认使用B+Tree，而不是Hash，二叉树，红黑树？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#2为什么索引结构默认使用b+tree而不是hash二叉树红黑树)  


B+tree：因为B树不管叶子节点还是非叶子节点，都会保存数据，这样导致在非叶子节点中能保存的指针数量变少（有些资料也称为扇出），指针少的情况下要保存大量数据，只能增加树的高度，导致IO操作变多，查询性能变低；

Hash：虽然可以快速定位，但是没有顺序，IO复杂度高。

二叉树：树的高度不均匀，不能自平衡，查找效率跟数据有关（树的高度），并且IO代价高。

红黑树：树的高度随着数据量增加而增加，IO代价高。


### [3、MySQL里记录货币用什么字段类型好](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#3mysql里记录货币用什么字段类型好)  


NUMERIC和DECIMAL类型被MySQL实现为同样的类型，这在SQL92标准允许。他们被用于保存值，该值的准确精度是极其重要的值，例如与金钱有关的数据。当声明一个类是这些类型之一时，精度和规模的能被(并且通常是)指定。

**例如：**

salary DECIMAL(9,2)

在这个例子中，9(precision)代表将被用于存储值的总的小数位数，而2(scale)代表将被用于存储小数点后的位数。

因此，在这种情况下，能被存储在salary列中的值的范围是从-9999999.99到9999999.99。


### [4、数据库自增主键可能遇到什么问题。](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#4数据库自增主键可能遇到什么问题。)  


使用自增主键对数据库做分库分表，可能出现诸如主键重复等的问题。解决方案的话，简单点的话可以考虑使用UUID哈

自增主键会产生表锁，从而引发问题

自增主键可能用完问题。


### [5、从锁的类别角度讲，MySQL都有哪些锁呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#5从锁的类别角度讲mysql都有哪些锁呢)  


从锁的类别上来讲，有共享锁和排他锁。

共享锁: 又叫做读锁。当用户要进行数据的读取时，对数据加上共享锁。共享锁可以同时加上多个。

排他锁: 又叫做写锁。当用户要进行数据的写入时，对数据加上排他锁。排他锁只可以加一个，他和其他的排他锁，共享锁都相斥。


### [6、索引失效情况？ ==校验SQL语句是否使用了索引方式为：](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#6索引失效情况-校验sql语句是否使用了索引方式为：)  


**在SQL语句前面使用explain关键字==**

**1、** like以%开头索引无效，当like以&结尾，索引有效。

**2、** or语句前后没有同事使用索引，当且仅当or语句查询条件的前后列均为索引时，索引生效。

**3、** 组合索引，使用的不是第一列索引时候，索引失效，即最左匹配规则。

**4、** 数据类型出现隐式转换，如varchar不加单引号的时候可能会自动转换为int类型，这个时候索引失效。

**5、** 在索引列上使用IS NULL或者 IS NOT NULL 时候，索引失效，因为索引是不索引空值得。

**6、** 在索引字段上使用，NOT、 <>、！= 、时候是不会使用索引的，对于这样的处理只会进行全表扫描。

**7、** 对索引字段进行计算操作，函数操作时不会使用索引。

**8、** 当全表扫描速度比索引速度快的时候不会使用索引。


### [7、优化特定类型的查询语句](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#7优化特定类型的查询语句)  


**平时积累吧：**

**1、** 比如使用select 具体字段代替 select *

**2、** 使用count(*) 而不是count(列名)

**3、** 在不影响业务的情况，使用缓存

**4、** explain 分析你的SQL


### [8、MySQL数据库作发布系统的存储，一天五万条以上的增量，预计运维三年,怎么优化？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#8mysql数据库作发布系统的存储一天五万条以上的增量预计运维三年,怎么优化)  


a、设计良好的数据库结构，允许部分数据冗余，尽量避免join查询，提高效率。

b、选择合适的表字段数据类型和存储引擎，适当的添加索引。

c、MySQL库主从读写分离。

d、找规律分表，减少单表中的数据量提高查询速度。

e。添加缓存机制，比如Memcached，apc等。

f、不经常改动的页面，生成静态页面。

g、书写高效率的SQL。比如 SELECT * FROM TABEL 改为 SELECT field_1, field_2, field_3 FROM TABLE.


### [9、MyISAM表格将在哪里存储，并且还提供其存储格式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#9myisam表格将在哪里存储并且还提供其存储格式)  


每个MyISAM表格以三种格式存储在磁盘上：

·“.frm”文件存储表定义

·数据文件具有“.MYD”（MYData）扩展名

索引文件具有“.MYI”（MYIndex）扩展名


### [10、为什么要优化](https://gitee.com/souyunku/DevBooks/blob/master/docs/MySQL/MySQL高级面试题，中级面试题，大汇总.md#10为什么要优化)  


**1、** 系统的吞吐量瓶颈往往出现在数据库的访问速度上

**2、** 随着应用程序的运行，数据库的中的数据会越来越多，处理时间会相应变慢

**3、** 数据是存放在磁盘上的，读写速度无法和内存相比

优化原则：减少系统瓶颈，减少资源占用，增加系统的反应速度


### 11、MySQL中都有哪些触发器？
### 12、SQL 约束有哪几种呢？
### 13、试述视图的优点？
### 14、说一下大表查询的优化方案
### 15、大表数据查询，怎么优化
### 16、慢查询日志
### 17、解释MySQL外连接、内连接与自连接的区别
### 18、MySQL的binlog有有几种录入格式？分别有什么区别？
### 19、使用索引查询一定能提高查询的性能吗？为什么
### 20、UNION与UNION ALL的区别？
### 21、你是否做过主从一致性校验，如果有，怎么做的，如果没有，你打算怎么做？
### 22、字段为什么要求定义为not null？
### 23、drop、delete与truncate的区别
### 24、主键、外键和索引的区别？
### 25、MySQL的复制原理以及流程
### 26、100.MySQL一条SQL加锁分析
### 27、存储引擎选择
### 28、drop、delete与truncate的区别
### 29、什么是脏读？幻读？不可重复读？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




