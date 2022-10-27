# Python最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、为什么Python执行速度慢，我们如何改进它？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#1为什么python执行速度慢我们如何改进它)  


Python代码执行缓慢的原因，是因为它是一种解释型语言。它的代码在运行时进行解释，而不是编译为本地语言。

为了提高Python代码的速度，我们可以使用CPython、Numba，或者我们也可以对代码进行一些修改。

**1、**  减少内存占用。

**2、**  使用内置函数和库。

**3、**  将计算移到循环外。

**4、**  保持小的代码库。

**5、**  避免不必要的循环


### [2、解释Python中的join()和split()函数](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#2解释python中的join和split函数)  


Join()能让我们将指定字符添加至字符串中。

```
>>> ','.join('12345')
```

运行结果：

```
‘1,2,3,4,5’
```

Split()能让我们用指定字符分割字符串。

```
>>> '1,2,3,4,5'.split(',')
```

运行结果：

```
[‘1’, ‘2’, ‘3’, ‘4’, ‘5’]
```


### [3、如何判断一个值是方法还是函数？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#3如何判断一个值是方法还是函数)  


**1、** 使用type()来判断，如果是method为方法，如果是function则是函数。

**2、** 与类和实例无绑定关系的function都属于函数（function）

**3、** 与类和实例有绑定关系的function都属于方法


### [4、写个函数接收一个文件夹名称作为参数，显示文件夹中文件的路径，以及其中包含的文件夹中文件的如今](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#4写个函数接收一个文件夹名称作为参数显示文件夹中文件的路径以及其中包含的文件夹中文件的如今)  


```python
# 方法一
import os
def Test1(rootDir):
list_dirs = os.walk(rootDir)
for root, dirs, files in list_dirs:
for d in dirs:
print(os.path.join(root, d))
for f in files:
print(os.path.join(root, f))
Test1(r'C:\Users\felix\Desktop\aaa')
print('#############')
# 方法二
import os
def Test2(rootDir):
paths=os.listdir(rootDir)
for lis in paths:
path=os.path.join(rootDir,lis)
print(path)
if os.path.isdir(path):
 Test2(path)
Test2(r'C:\Users\felix\Desktop\aaa')
```


### [5、使用yield实现一个协程](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#5使用yield实现一个协程)  


```python
def consumer():
r = ''
while True:
n = yield r
if n is None:
return
print('[CONSUMER] Consuming %s...' % n)
r = '200 OK'

def produce(c):
c.send(None)
n = 0
while n < 5:
n = n + 1
print('[PRODUCER] Producing %s...' % n)
r = c.send(n)
print('[PRODUCER] Consumer return: %s' % r)
c.close()

c = consumer()
produce(c)
```


### [6、把a='aaabbcccdddde'这种形式的字符串，压缩成a3b2c3d4e1这种形式。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#6把a='aaabbcccdddde'这种形式的字符串压缩成a3b2c3d4e1这种形式。)  


```python
a='aaabbcccdddde'
aa=''
for i in sorted(list(set(a)),key=a.index):
aa=aa+i+str(a.count(i))
print(aa)
```


### [7、什么是反射，以及应用场景](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#7什么是反射以及应用场景)  


[什么是反射的解释](https://www.cnblogs.com/IT-Scavenger/p/9394306.html)

**1、** 反射就是通过字符串的形式，导入模块；通过字符串的形式，去模块寻找指定函数，并执行。利用字符串的形式去对象（模块）中操作（查找/获取/删除/添加）成员，一种基于字符串的事件驱动！

**2、** 应用场景：当我们动态的输入一个模块名的时候就可以使用到反射。

**3、** 通过hasattr，getattr，delattr，setattr等四个函数来操作


### [8、文件操作时，xreadlines和readlines的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#8文件操作时xreadlines和readlines的区别)  


**1、** xreadlines返回的是一个生成器

**2、** readlines返回的是一个列表


### [9、Python中append，insert和extend的区别?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#9python中appendinsert和extend的区别)  


append：在列表末尾添加新元素。

insert：在列表的特定位置添加元素。

extend：通过添加新列表来扩展列表。

```
numbers = [1,2,3,4,5]
numbers.append(6)
print(numbers)
>[1,2,3,4,5,6]

## insert(position,value)
numbers.insert(2,7)  
print(numbers)
>[1,2,7,4,5,6]

numbers.extend([7,8,9])
print(numbers)
>[1,2,7,4,5,6,7,8,9]

numbers.append([4,5])
>[1,2,7,4,5,6,7,8,9,[4,5]]
```


### [10、简述事务及其特性](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，2021年面试题及答案汇总.md#10简述事务及其特性)  


事务是用户定义的一个数据库操作序列，这些操作要么全做要么全不做，是一个不可分割的工作单位

事务具有4个特性：原子性、一致性、隔离性和持续性。

**1、** 原子性：事务是数据库的逻辑工作单位，事务中包括的诸操作要么都做，要么都不做。

**2、** 一致性：事务执行的结果必须是使数据库从一个一致性状态变到另一个一致性状态。

**3、** 隔离性：一个事务的执行不能被其他事务干扰。即一个事务内部的操作及使用的数据对其他并发事务是隔离的，并发执行的各个事务之间不能互相干扰。

**4、** 持续性：持续性也称永久性，指一个事务一旦提交，它对数据库中数据的改变就应该是永久性的。接下来的其他操作或故障不应该对其执行结果有任何影响。


### 11、什么是cdn
### 12、将列表按照下列规则排序：
### 13、MySQL索引种类
### 14、什么是socket？简述基于tcp协议的socket通信流程？
### 15、a = dict(zip(('a','b','c','d','e'),(1,2,3,4,5))) 请问a是什么？
### 16、char和varchar的区别
### 17、编写程序，打印斐波那契数列的前十项
### 18、列举创建索引但是无法命中索引的情况
### 19、手写一个栈
### 20、简述数据库分库分表
### 21、找出两个列表中相同的元素和不同的元素
### 22、写一个函数，计算出以下字母所代表的数字，每个字母值不一样
### 23、怎么移除一个字符串中的前导空格？
### 24、is和==的区别
### 25、简述SQL注入原理，以及如何在代码层面房子sql注入
### 26、python解释器种类以及特点
### 27、traceroute使用哪种网络协议
### 28、简述python字符串的驻留机制
### 29、如何实现"1.2.3"变成['1','2','3']?
### 30、isinstance和type的作用





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




