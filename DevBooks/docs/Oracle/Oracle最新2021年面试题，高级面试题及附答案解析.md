# Oracle最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、如何重构索引？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#1如何重构索引)  


ALTER INDEX <index_name> REBUILD;


### [2、说说Oracle中经常使用到的函数](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#2说说oracle中经常使用到的函数)  


length长度、lower小写、upper大写、to_date转化日期、to_char转化字符、to_number转化数字Ltrim去左边空格、rtrim去右边空格、substr截取字符串、add_month增加或减掉月份、


### [3、解释data block , extent 和 segment的区别(这里建议用英文术语)](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#3解释data-block-,-extent-和-segment的区别这里建议用英文术语)  


data block是数据库中最小的逻辑存储单元。当数据库的对象需要更多的物理存储空间时，连续的data block就组成了extent . 一个数据库对象拥有的所有extents被称为该对象的segment.


### [4、给出数据库正常启动所经历的几种状态 ?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#4给出数据库正常启动所经历的几种状态-)  


STARTUP NOMOUNT ?C 数据库实例启动

STARTUP MOUNT - 数据库装载

STARTUP OPEN ?C 数据库打开


### [5、如何转换init.ora到spfile?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#5如何转换initora到spfile)  


使用create spfile from pfile 命令.


### [6、举出3种可以收集three advisory statistics](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#6举出3种可以收集three-advisory-statistics)  


Buffer Cache Advice, Segment Level Statistics, Timed Statistics


### [7、哪个VIEW用来检查数据文件的大小？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#7哪个view用来检查数据文件的大小)  


DBA_DATA_FILES


### [8、回滚段的作用是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#8回滚段的作用是什么)  


事务回滚：当事务修改表中数据的时候，该数据修改前的值(即前影像)会存放在回滚段中，当用户回滚事务(ROLLBACK)时，ORACLE将会利用回滚段中的数据前影像来将修改的数据恢复到原来的值。

事务恢复：当事务正在处理的时候，例程失败，回滚段的信息保存在undo表空间中，ORACLE将在下次打开数据库时利用回滚来恢复未提交的数据。

**1、** 读一致性：当一个会话正在修改数据时，其他的会话将看不到该会话未提交的修改。

**2、** 当一个语句正在执行时，该语句将看不到从该语句开始执行后的未提交的修改(语句级读一致性)。

**3、** 当ORACLE执行Select语句时，ORACLE依照当前的系统改变号(SYSTEM CHANGE NUMBER-SCN)。

**4、** 来保证任何前于当前SCN的未提交的改变不被该语句处理。可以想象：当一个长时间的查询正在执行时。

**5、** 若其他会话改变了该查询要查询的某个数据块，ORACLE将利用回滚段的数据前影像来构造一个读一致性视图。


### [9、你必须利用备份恢复数据库，但是你没有控制文件，该如何解决问题呢？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#9你必须利用备份恢复数据库但是你没有控制文件该如何解决问题呢)  


重建控制文件，用带backup control file 子句的recover 命令恢复数据库。


### [10、如何变动数据文件的大小？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题，高级面试题及附答案解析.md#10如何变动数据文件的大小)  


ALTER DATABASE DATAFILE <datafile_name> RESIZE <new_size>;


### 11、解释data block , extent 和 segment的区别（这里建议用英文术语）
### 12、存储过程 、函数 、游标 在项目中怎么用的：
### 13、用于网络连接的2个文件？
### 14、如何转换init.ora到spfile?
### 15、给出在STAR SCHEMA中的两种表及它们分别含有的数据
### 16、提示窗体中触发的顺序是什么?
### 17、如何在不影响子表的前提下，重建一个母表
### 18、解释什么是Partitioning（分区）以及它的优点。
### 19、如何建立一个备份控制文件?
### 20、解释冷备份和热备份的不同点以及各自的优点
### 21、解释归档和非归档模式之间的不同和它们各自的优缺点
### 22、如何进行强制LOG SWITCH?
### 23、如何生成explain plan?
### 24、说明如何使用相同的LOV 2列?
### 25、Coalescing做了什么？
### 26、ORA-01555的应对方法？
### 27、解释什么是死锁，如何解决Oracle中的死锁？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




