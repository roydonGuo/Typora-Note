# Oracle最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、给出在STAR SCHEMA中的两种表及它们分别含有的数据](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#1给出在star-schema中的两种表及它们分别含有的数据)  


Fact tables 和dimension tables. fact table包含大量的主要的信息而dimension tables 存放对fact table 某些属性描述的信息


### [2、如何生成explain plan?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#2如何生成explain-plan)  


运行utlxplan.sql. 建立plan 表

针对特定SQL语句，使用 explain plan set statement_id = 'tst1' into plan_table运行utlxplp.sql 或 utlxpls.sql察看explain plan


### [3、Oracle中function和procedure的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#3oracle中function和procedure的区别)  


**1、** 可以理解函数是存储过程的一种

**2、** 函数可以没有参数,但是一定需要一个返回值，存储过程可以没有参数,不需要返回值

**3、** 函数return返回值没有返回参数模式，存储过程通过out参数返回值, 如果需要返回多个参数则建议使用存储过程

**4、** 在sql数据操纵语句中只能调用函数而不能调用存储过程


### [4、如何使用Oracle的游标？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#4如何使用oracle的游标)  


**1、** oracle中的游标分为显示游标和隐式游标

**2、** 显示游标是用cursor...is命令定义的游标，它可以对查询语句(select)返回的多条记录进行处理；隐式游标是在执行插入 (insert)、删除(delete)、修改(update)和返回单条记录的查询(select)语句时由PL/SQL自动定义的。

**3、** 显式游标的操作：打开游标、操作游标、关闭游标；PL/SQL隐式地打开SQL游标，并在它内部处理SQL语句，然后关闭它


### [5、解释什么是Oracle Forms?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#5解释什么是oracle-forms)  


Oracle Forms是用于创建与Oracle数据库交互的软件产品。它有一个IDE，包括一个属性表，对象导航器和使用PL/SQL的代码编辑器。


### [6、集合操作符](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#6集合操作符)  


**1、** Union ： 不包含重复值，默认按第一个查询的第一列升序排列。

**2、** Union All : 完全并集包含重复值。不排序。

**3、** Minus 不包含重复值，不排序。


### [7、说下 oracle的锁又几种,定义分别是什么;](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#7说下-oracle的锁又几种,定义分别是什么;)  


**1、** 行共享锁 (ROW SHARE)

**2、** 行排他锁(ROW EXCLUSIVE)

**3、** 共享锁(SHARE)

**4、** 共享行排他锁(SHARE ROW EXCLUSIVE)

**5、** 排他锁(EXCLUSIVE)


### [8、提到一个项目的“验证LOV”属性?提到lov和list项目有什么区别?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#8提到一个项目的“验证lov属性提到lov和list项目有什么区别)  


当验证的LOV设置为True时，Oracle Forms将文本项的当前值与LOV中显示的第一列中的值进行比较。LOV是列表项的属性。列表项只能有一列，而lov可以有一个或多个列。


### [9、FACT Table上需要建立何种索引？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#9fact-table上需要建立何种索引)  


位图索引（bitmap index）


### [10、pctused and pctfree 表示什么含义有什么作用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Oracle/Oracle最新2021年面试题附答案解析，大汇总.md#10pctused-and-pctfree-表示什么含义有什么作用)  


pctused与pctfree控制数据块是否出现在freelist中,pctfree控制数据块中保留用于update的空间,当数据块中的free space小于pctfree设置的空间时，该数据块从freelist中去掉,当块由于dml操作free space大于pct_used设置的空间时,该数据库块将被添加在freelist链表中。


### 11、描述tablespace和datafile之间的关系
### 12、列出Oracle Forms配置文件?
### 13、如何建立一个备份控制文件？
### 14、oracle的锁又几种,定义分别是什么;
### 15、Oracle的游标在存储过程里是放在begin与end的里面还是外面？
### 16、数据库的三大范式是什么？
### 17、触发器的作用有哪些？
### 18、Oracle的导入导出有几种方式，有何区别？
### 19、创建用户时，需要赋予新用户什么权限才能使它联上数据库。
### 20、SGA主要有那些部分，主要作用是什么?
### 21、怎样创建一个一个索引,索引使用的原则,有什么优点和缺点
### 22、如何启动SESSION级别的TRACE
### 23、解释TABLE Function的用途
### 24、说下 Oracle中有哪几种文件？
### 25、解释$$ORACLE_HOME和$$ORACLE_BASE的区别？
### 26、不借助第三方工具，怎样查看sql的执行计划
### 27、如何判断哪个session正在连结以及它们等待的资源？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




