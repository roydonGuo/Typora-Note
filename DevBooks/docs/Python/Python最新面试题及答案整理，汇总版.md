# Python最新面试题及答案整理，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、python的垃圾回收机制](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#1python的垃圾回收机制)  


[python垃圾回收机制详解](https://testerhome.com/topics/16556)

**1、** 概述：python采用的是引用计数机制为主，标记-清除和分代收集两种机制为辅的策略

**2、** 引用计数：

**3、** 每当新的引用指向该对象时，引用计数加1，当对该对象的引用失效时，引用计数减1，当对象的引用计数为0时，对象被回收。缺点是，需要额外的空间来维护引用计数，并且无法解决对象的循环引用。

**4、** 分代回收：（具体见上面链接）

**5、** 以时间换空间的回收方式

**6、** 标记清除：

**7、** 活动对象会被打上标记，会把那些没有被打上标记的非活动对象进行回收。


### [2、你对Python类中的self有什么了解？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#2你对python类中的self有什么了解)  


self表示类的实例。

通过使用self关键字，我们可以在Python中访问类的属性和方法。

注意，在类的函数当中，必须使用self，因为类中没有用于声明变量的显式语法。


### [3、求出以下代码的输出结果](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#3求出以下代码的输出结果)  


```python
mydict={'a':1,'b':2}
def func(d):
d['a']=0
return d

func(mydict)
mydict['c']=2
print(mydict)
```

结果

> {'a': 0, 'b': 2, 'c': 2}



### [4、解决哈希冲突的算法有哪几种？分别有什么特点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#4解决哈希冲突的算法有哪几种分别有什么特点)  


[哈希冲突参考](https://blog.csdn.net/seulzz/article/details/77163878)

**1、** 开放定址法

**2、** 再哈希法

**3、** 链地址法

**4、** 建立公共溢出区


### [5、解释Python中的help()和dir()函数](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#5解释python中的help和dir函数)  


Help()函数是一个内置函数，用于查看函数或模块用途的详细说明：

```
>>> import copy
>>> help(copy.copy)
```

运行结果为：

```
Help on function copy in module copy:

 
 
copy(x)
 
Shallow copy operation on arbitrary Python objects.
 
See the module’s __doc__ string for more info.
```

Dir()函数也是Python内置函数，dir() 函数不带参数时，返回当前范围内的变量、方法和定义的类型列表；带参数时，返回参数的属性、方法列表。

以下实例展示了 dir 的使用方法：

```
>>> dir(copy.copy)
```

运行结果为：

```
[‘__annotations__’, ‘__call__’, ‘__class__’, ‘__closure__’, ‘__code__’, ‘__defaults__’, ‘__delattr__’, ‘__dict__’, ‘__dir__’, ‘__doc__’, ‘__eq__’, ‘__format__’, ‘__ge__’, ‘__get__’, ‘__getattribute__’, ‘__globals__’, ‘__gt__’, ‘__hash__’, ‘__init__’, ‘__init_subclass__’, ‘__kwdefaults__’, ‘__le__’, ‘__lt__’, ‘__module__’, ‘__name__’, ‘__ne__’, ‘__new__’, ‘__qualname__’, ‘__reduce__’, ‘__reduce_ex__’, ‘__repr__’, ‘__setattr__’, ‘__sizeof__’, ‘__str__’, ‘__subclasshook__’]
```


### [6、什么是断言(assert)?应用场景？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#6什么是断言assert应用场景)  


[断言的参考](https://blog.csdn.net/shujuanyaning/article/details/47184541)

assert是用来检查一个条件，如果它为真，就不做任何事。如果它为假，则会抛出AssertError并且包含错误信息。

**应用场景**：

**1、** 防御型编程

**2、** 运行时检查程序逻辑

**3、** 检查约定

**4、** 程序常量

**5、** 检查文档


### [7、python代码如何获取命令行参数](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#7python代码如何获取命令行参数)  


[获取命令行参数的方法参考](https://www.cnblogs.com/ouyangpeng/p/8537616.html)

**1、** 使用sys模块

通过sys.argv来获取

**2、** 使用getopt模块


### [8、给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。例如：'ababab',返回True，'ababa'，返回False](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#8给定一个非空的字符串判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母并且长度不超过10000。例如：'ababab',返回true'ababa'返回false)  


```python
def solution(s):
ll=len(s)
for i in range(1,ll//2+1):
if ll % i == 0:
j=0
while s[:i]==s[j:j+i] and j<ll:
    j=j+i
if j==ll:
    return True
return False

print(solution('abababa'))
```


### [9、写python爬虫分别用到了哪些模块？分别有什么用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#9写python爬虫分别用到了哪些模块分别有什么用)  


模块

request，发起请求

pyquery，解析html数据

beautifulsoup，解析html数据

aiohttp，异步发送请求

框架

pyspider，web界面的爬虫框架

scrapy，爬虫框架

selenium，模拟浏览器的爬虫框架


### [10、Python有哪些特点和优点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案整理，汇总版.md#10python有哪些特点和优点)  


作为一门编程入门语言，Python主要有以下特点和优点：

**1、** 可解释

**2、** 具有动态特性

**3、** 面向对象

**4、** 简明简单

5、开源

**6、** 具有强大的社区支持

当然，实际上Python的优点远不止如此，


### 11、如何实现响应式布局
### 12、Redis默认多少个db
### 13、简述触发器、函数、视图和存储过程
### 14、什么是switch语句。如何在Python中创建switch语句？
### 15、一行代码实现删除列表中的所有的重复的值
### 16、Redis如何实现事务
### 17、现有mydict和变量onekey，请写出从mydict中取出onekey的值的方法
### 18、如果已经建立了TCP连接，但是客户端突然出现故障了怎么办
### 19、解释Python中的Filter？
### 20、python中进制转换
### 21、列举你所了解的所有Python2和Python3的区别
### 22、*arg和**kwargs的作用
### 23、MySQL如何创建索引
### 24、什么时GIL锁
### 25、TCP和UDP的区别
### 26、编写一个函数实现十进制转62进制，分别用0-9A-Za-z,表示62位字母
### 27、python如何定义函数时如何书写可变参数和关键字参数？
### 28、Python中的pass语句是什么？
### 29、Python有哪些应用？
### 30、GIL锁对python性能的影响





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




