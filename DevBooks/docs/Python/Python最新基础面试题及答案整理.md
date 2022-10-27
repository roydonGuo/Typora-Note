# Python最新基础面试题及答案整理


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、使用python将数据库的student表中的数据写入db.txt](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#1使用python将数据库的student表中的数据写入dbtxt)  


```python
import pyMySQL
connect=pyMySQL.Connect(
host='',
port=,
user='',
passwd='',
db='',
charset='',
)

cursor=connect.cursor()
sql='select from student'
cursor.execute(sql)
students=cursor.fetchall()

with open('db.txt','w') as f:
for student in students:
f.write(student)

cursor.close()
connect.close()
```


### [2、了解过Hbase，DB2，SQLServer，Access吗](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#2了解过hbasedb2sqlserveraccess吗)  


**1、** Hbase：HBase是一个分布式的、面向列的开源数据库

**2、** DB2：一套关系型数据库管理系统，

**3、** SQLServer：SQL Server是由Microsoft开发和推广的关系数据库管理系统

**4、** Sccess：Access是由微软发布的关系数据库管理系统。


### [3、解释一下Python中的继承？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#3解释一下python中的继承)  


继承(inheritance)允许一个类获取另一个类的所有成员和属性。继承提供代码可重用性，可以更轻松地创建和维护应用程序。

被继承的类称为超类，而继承的类称为派生类/子类。


### [4、什么是并发和并行](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#4什么是并发和并行)  


**1、** 并发:指应用能够交替执行不同的任务,其实并发有点类似于多线程的原理,多线程并非是同时执行多个任务,如果你开两个线程执行,就是在你几乎不可能察觉到的速度不断去切换这两个任务,已达到"同时执行效果",其实并不是的,只是计算机的速度太快,我们无法察觉到而已.

**2、** 并行:指应用能够同时执行不同的任务,

**3、** 并发是多个事件在同一时间段执行，并行是多个事件在统一时间点执行。


### [5、json序列化时可以处理的数据类型有哪些？如何定制支持datetime类型？序列化时，遇到中文转成unicode，如何保持中文形式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#5json序列化时可以处理的数据类型有哪些如何定制支持datetime类型序列化时遇到中文转成unicode如何保持中文形式)  


**1、** 可以处理的数据类型是 string、int、list、tuple、dict、bool、null

**2、** 通过自定义时间序列化转换器

```python
import json
from json import JSONEncoder
from datetime import datetime
class ComplexEncoder(JSONEncoder):
def default(self, obj):
if isinstance(obj, datetime):
return obj.strftime(‘%Y-%m-%d %H:%M:%S‘)
else:
return super(ComplexEncoder,self).default(obj)
d = { ‘name‘:‘alex‘,‘data‘:datetime.now()}
print(json.dumps(d,cls=ComplexEncoder))
# {"name": "alex", "data": "2018-05-18 19:52:05"}
```

**3、** 使用ensure_ascii=False参数


### [6、二叉树是非线性结构，栈和队列以及线性表都是线性结构，对吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#6二叉树是非线性结构栈和队列以及线性表都是线性结构对吗)  


对的


### [7、如何以就地操作方式打乱一个列表的元素？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#7如何以就地操作方式打乱一个列表的元素)  


为了达到这个目的，我们从random模块中导入shuffle()函数。

```
>>> from random import shuffle
>>> shuffle(mylist)
>>> mylist
```

运行结果：

```
[3, 4, 8, 0, 5, 7, 6, 2, 1]
```


### [8、对列表[3,1,-4,-2]按照绝对值排序](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#8对列表[3,1,-4,-2]按照绝对值排序)  


```python
lis=[3,1,-4,-2]
lis=sorted(lis,key=lambda x:abs(x))
print(lis)
```


### [9、Python中的字典是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#9python中的字典是什么)  


字典是C++和Java等编程语言中所没有的东西，它具有键值对。

```
>>> roots={25:5,16:4,9:3,4:2,1:1}
>>> type(roots)
<class 'dict'>
>>> roots[9]
```

运行结果为：

```
3
```

字典是不可变的，我们也能用一个推导式来创建它。

```
>>> roots={x**2:x for x in range(5,0,-1)}
>>> roots
```

运行结果：

```
{25: 5, 16: 4, 9: 3, 4: 2, 1: 1}
```


### [10、类和对象有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新基础面试题及答案整理.md#10类和对象有什么区别)  


类(Class)被视为对象的蓝图。类中的第一行字符串称为doc字符串，包含该类的简短描述。

在Python中，使用class关键字可以创建了一个类。一个类包含变量和成员组合，称为类成员。

对象(Object)是真实存在的实体。在Python中为类创建一个对象，我们可以使用obj = CLASS_NAME()

例如：obj = num()

使用类的对象，我们可以访问类的所有成员，并对其进行操作。

```
class Person:
    """ This is a Person Class"""
    # varable
    age = 10
    def greets(self):
        print('Hello')


# object
obj = Person()
print(obj.greet)
----------------------------------------
Hello
```


### 11、如何在函数中设置一个全局变量？
### 12、解释一下Python中的成员运算符
### 13、什么是asyncio
### 14、简述线程死锁是怎么造成的。如何避免？
### 15、JavaScript(或者jQuery)如何选择一个id为main的容器
### 16、什么是codis
### 17、用尽量简洁的方法将二维数组合并成一维数组
### 18、阅读以下代码，写输出结果
### 19、判断dict中有没有某个key。
### 20、编写程序，检查序列是否为回文
### 21、手写一个队列
### 22、MySQL慢日志
### 23、列举面向对象中带双下划线的特殊方法
### 24、python和java、php、c、c#、c++ 等其他语言对比？
### 25、描述以下字典的items()方法和iteritems()方法有啥不同？
### 26、发生粘包现象如何处理？
### 27、什么是pickling和unpickling？
### 28、Python区分大小写吗？
### 29、Python代码是如何执行的？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




