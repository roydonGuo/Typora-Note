# Python高级面试题及答案，企业真面试题


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、MySQL的增删改查](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#1mysql的增删改查)  


**增**

**指定字段名**

语法：INSERT INTO 表名（字段名1，字段名2，…）VALUES（值1，值2，…）；

举例：INSERT INTO student(id,name,grade) VALUES(1,'zhangshan',98);

**不指定字段名**

语法：INSERT INTO 表名 VALUES(值11，值2，…）；

举例：INSERT INTO student VALUES (2,'lisi',62);

**其他写法**

语法：INSERT INTO 表名 SET 字段名1=值1[,字段名2=值2，…]

举例：INSERT INTO student SET id=4，name='zhaoliu',grade=72;

**同时添加多条数据**

语法：INSERT INTO 表名[(字段名1，字段名2，…)] VALUES （值1，值2，…），（值1，值2，…），…（值1，值2，…）

举例：INSERT INTO student VALUES (5，‘lilei’,99), (6,'hanmeimei',87), (8,'poly',76);

**删**

**删除部分数据**

语法：DELETE FROM 表名 [WHERE 条件表达式]

命令：DELETE  FROM student WHERE id=7;

**删除全部数据**

语法：DELETE FROM 表名

命令：DELETE FROM student；

**推荐的删除全部数据**

语法：TRUNCTE [TABLE ] 表名

举例：TRUNCATE TABLE student

**改**

**更新部分数据**

语法：UPDATE 表名 SET 字段名1=值1，[ ，字段名2=值2，…] [ WHERE 条件表达式 ]

命令：UPDATE student SET name=‘caocao’,grade=50 WHERE id=1;

**更新全部数据**

语法：UPDATE 表名 SET 字段名=值

命令：UPDATE student SET grade=80；

**查**

**查询所有字段**

语法：SELECT 字段名1，字段名2，… FROM 表名 （该语法也可以查询部分字段）

语法：SELECT FROM 表名；

**按条件查询**

语法：SELECT 字段名1，字段名2，… FROM 表名 WHERE 条件表达式

命令：SELECT id，name FROM student2  WHERE id=4;

**带IN关键字的查询**

**1、** 语法：SELECT | 字段名1，字段名2，… FROM 表名 WHERE 字段名 [ NOT ]  IN （元素1，元素2，…）

**2、** 命令：SELECT FROM student2 WHERE id IN （1,2,3）；

**3、** 带 BETWEEN AND  关键字的查询

**4、** 语法：SELECT | { 字段名1，字段名2，… } FROM  表名 WHERE 字段名 [ NOT ] BETWEEN  值1  AND  值2；

**5、** 命令：SELECT id,name FROM students WHERE id BETWEEN 2 AND 5;

**空值查询**

语法：SELECT | 字段名1，字段名2，… FROM 表名 WHERE 字段名 IS [ NOT ] NULL

命令：SELECT FROM student2 WHERE gender IS NULL;

**带 DISTINCT 关键字的查询**

语法：SELECT DISTINCT 字段名 FROM 表名；

命令：SELECT DISTINCT gender FROM student2;

**带 LIKE 关键字的查询**

语法：SELECT | 字段名1，字段名2，… FROM 表名 WHERE 字段名 [ NOT ] LIKE ‘匹配字符串’;

**注意：%表示匹配任意长度的字符串，_表示匹配单个字符串**

**3、** 命令：SELECT id,name FROM student2  WHERE name LIKE "S%";

**4、** 命令：SELECT id,name FROM student2 WHERE name LIKE 'w%g';

**5、** 命令：SELECT id,name FROM student2 WHERE name NOT LIKE '%y%';

**6、** 命令：SELECT FROM student2 WHERE name LIKE 'wu_ong';

**带 AND 关键字的多条件查询**

**1、** 语法：SELECT | 字段名1，字段名2，… FROM 表名 WHERE 条件表达式1 AND 条件表达式2 [ … AND 条件表达式 n ];

**2、** 命令：SELECT id,name FROM student2 WHERE id<5 AND gender='女';

**带 OR 关键字的多条件查询**

**1、** 语法：SELECT | 字段名1，字段名2，… FROM 表名 WHERE 条件表达式1 OR 条件表达式2 [ … OR 条件表达式 n ];

**2、** 命令：SELECT id,name ,gender FROM student2 WHERE id<3 OR gender='女';

**AND和OR一起使用时，AND的优先级高于OR**

**聚合函数**

**COUNT()函数：统计记录的条数**

语法：SELECT COUNT(*) FROM 表名举例：

命令：SELECT COUNT(*) FROM student2;

**SUM()函数：求出表中某个字段所有值的总和**

语法：SELECT  SUM(字段名) FROM 表名；

命令：SELECT SUM(grade) FROM student2;

**AVG()函数：求出表中某个字段所有值的平均值**

语法：SELECT AVG(字段名) FROM 表名；

命令：SELECT AVG(grade) FROM student2;

**MAX()函数：求出表中某个字段所有值的最大值**

语法：SELECT MAX(字段名) FROM 表名；

命令：SELECT MAX(grade) FROM student2;

**MIN()函数：求出表中某个字段所有值的最小值**

语法：SELECT MIN(字段名) FROM 表名；

命令：SELECT MIN(grade) FROM student2;

**对查询结果进行排序**

语法：SELECT 字段名1，字段名2，… FROM 表名 ORDER BY 字段名1 [ ASC | DESC ],字段名2 [ ASC | DESC ]

(升序)命令：SELECT FROM student2 ORDER BY grade;

(降序)命令：命令：SELECT FROM student2 ORDER BY grade DESC;

**分组查询**

语法：SELECT  字段名1，字段名2，… FROM 表名 GROUP BY 字段名1，字段名2，… [ HAVING 条件表达式 ];

**单独使用 GROUP BY 进行分组**

命令：SELECT FROM student2 GROUP BY gender;

**GROUP BY 和聚合函数一起使用**

命令：SELECT COUNT(*) ,gender FROM student2 GROUP BY gender;

**GROUP BY 和 HAVING 关键字一起使用**

命令：SELECT sum(grade),gender FROM student2 GROUP BY gender HAVING SUM(grade) < 300;

**使用 LIMIT 限制查询结果的数量**

语法：SELECT 字段名2，字段名2，… FROM 表名 LIMIT [ OFFSET ,] 记录数

(从0开始的4条)命令：SELECT FROM student LIMIT 4;

(从第五条开始的4条)命令：SELECT FROM student2 ORDER BY grade DESC LIMIT 4,4;

**为表和字段取别名**

语法：SELECT FROM 表名 [ AS ] 别名；

命令：SELECT FROM student2 AS s WHERE s.gender='女';

**为字段取别名**

语法：SELECT 字段名 [ AS ] 别名 [ ,字段名 [AS] 别名，…]  FROM 表名 ；

命令：SELECT name AS stu_name,gender AS stu_gender FROM student2;


### [2、编写程序，检查数字是否为Armstrong](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#2编写程序检查数字是否为armstrong)  


将每个数字依次分离，并累加其立方(位数)。

最后，如果发现总和等于原始数，则称为阿姆斯特朗数(Armstrong)。

```
num = int(input("Enter the number:\n"))
order = len(str(num))

sum = 0
temp = num

while temp > 0:
   digit = temp % 10
   sum += digit ** order
   temp //= 10

if num == sum:
   print(num,"is an Armstrong number")
else:
   print(num,"is not an Armstrong number")
```


### [3、pass的使用](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#3pass的使用)  


通常用来标记一个还未写的代码的位置，pass不做任何事情，一般用来做占位语句，保持程序结构的完整性


### [4、MySQL的建表语句](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#4mysql的建表语句)  


```mysql
#创建表，例子
#所谓的建表就是声明列的过程,所以要首先分析列
create table member(
                       id int unsigned auto_increment primary key,
                       username varchar(20) not null default '',
                       gender char(1) not null default '',
                       weight tinyint unsigned not null default 0,
                       birth date not null default '0000-00-00',
                       salary decimal(8,2) not null default 0.00,
                       lastlogin int unsigned not null default 0
)engine myisam charset utf8;
```


### [5、请列出至少5个PEP8规范](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#5请列出至少5个pep8规范)  


**1、** 每个缩进级别使用4个空格

**2、** 每行代码的最大长度限制为79个字符

**3、** 若是导入多个库函数，应该分开依次导入

**4、** 道路应按照以下顺序导入

a、标准库导入

b、相关的第三方库导入

c、本地应用程序的库导入

**1、** 在表达式中避免无关的空格

**2、** 在括号或者大括号内

**3、** 在尾随逗号和后面的右括号之间

**4、** 在逗号，分号或者冒号前面

**5、** 函数名的与后面的参数的括号之间

**6、** 代码更改时，相应的注释也要随之更改

**7、** 命名要规范，通俗易懂


### [6、数据库锁的作用](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#6数据库锁的作用)  


**锁分为三种：乐观锁，悲观锁和共享锁**

数据库和操作系统一样，是一个多用户使用的共享资源。当多个用户并发地存取数据 时，在数据库中就会产生多个事务同时存取同一数据的情况。若对并发操作不加控制就可能会读取和存储不正确的数据，破坏数据库的一致性。加锁是实现数据库并 发控制的一个非常重要的技术。在实际应用中经常会遇到的与锁相关的异常情况，当两个事务需要一组有冲突的锁，而不能将事务继续下去的话，就会出现死锁，严 重影响应用的正常执行。


### [7、生成器与函数的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#7生成器与函数的区别)  


生成器和函数的主要区别在于函数 return a value，生成器 yield a value同时标记或记忆point of the yield 以便于在下次调用时从标记点恢复执行。 yield 使函数转换成生成器，而生成器反过来又返回迭代器。

```python
# 简单实现生成器
def dec():
n=0
for i in range(10):
yield n
n+=i

for i in dec():
print(i)
```


### [8、MySQL常见的函数](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#8mysql常见的函数)  


**1、** ABS(x)：返回x的绝对值

**2、** ROUND(x)：返回参数x的四舍五入的一个整数

**3、** TRIM(str)：去除字符串两边的空白

**4、** COUNT()：返回值的个数

**5、** AVG()：返回平均值

**6、** SUM()：求和


### [9、在python中如何拷贝一个对象，并说明他们之间的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#9在python中如何拷贝一个对象并说明他们之间的区别)  


**1、** 赋值（=），就是创建了对象的一个新的引用，修改其中任意一个变量都会影响到另一个。

**2、** 浅拷贝：创建一个新的对象，但它包含的是对原始对象中包含项的引用（copy模块的copy()函数）

**3、** 深拷贝：创建一个新的对象，并且递归的复制它所包含的对象（修改其中一个，另外一个不会改变）（copy模块的deep.deepcopy()函数）


### [10、讲讲Python中的位运算符](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python高级面试题及答案，企业真面试题.md#10讲讲python中的位运算符)  


该运算符按二进制位对值进行操作。

**1、**   与（&），按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0

```
>>> 0b110 & 0b010
2
```

**2、** 或（|），按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。

```
>>> 3|2
3
```

**3、** 异或（^），按位异或运算符：当两对应的二进位相异时，结果为1

```
>>> 3^2
1
```

**4、** 取反（~），按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1

```
>>> ~2
-3
```

**5、** 左位移（<<），运算数的各二进位全部左移若干位，由 << 右边的数字指定了移动的位数，高位丢弃，低位补0

```
>>> 1<<2
4
```

**6、** 右位移（>>），把">>"左边的运算数的各二进位全部右移若干位，>> 右边的数字指定了移动的位数

```
>>> 4>>2
1
```

更多关于运算符的知识，参考这里：

[戳这里](https://data-flair.training/blogs/python-operators/)


### 11、Redis如何实现主从复制？以及数据同步机制？
### 12、什么是索引合并
### 13、有如下代码：
### 14、什么是封装？
### 15、简述python的深浅拷贝
### 16、什么是haproxy？
### 17、Redis是单进程单线程的吗？
### 18、有一个多层嵌套的列表A=[1,2,3,[4,1,['j1',1,[1,2,3,'aa']]]],请写一段代码将A中的元素全部打印出来
### 19、python哪些类型的数据才能作为字典的key？
### 20、Python是否有main函数？
### 21、什么是twisted框架
### 22、你了解哪些数据库优化方案
### 23、vue中的路由拦截器的作用
### 24、实现一个装饰器，限制该函数被调用的频率，如10秒一次
### 25、请编写一个函数将ip地址转换成一个整数。如10.3.9.12转换成00001010 00000011 00001001 00001100，然后转换成整数
### 26、Python中OOPS是什么？
### 27、22、iterables和iterators之间的区别？
### 28、如何实现['1','2','3']变成[1,2,3]
### 29、Python中的单引号和双引号有什么区别？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




