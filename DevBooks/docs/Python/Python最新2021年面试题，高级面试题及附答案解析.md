# Python最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是Twemproxy](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#1什么是twemproxy)  


Twemproxy是一种代理分片机制，由Twitter开源。Twemproxy作为代理，可接受来自多个程序的访问，按照路由规则，转发给后台的各个Redis服务器，再原路返回。该方案很好的解决了单个Redis实例承载能力的问题。当然，Twemproxy本身也是单点，需要用Keepalived做高可用方案。通过Twemproxy可以使用多台服务器来水平扩张Redis服务，可以有效的避免单点故障问题。虽然使用Twemproxy需要更多的硬件资源和在Redis性能有一定的损失（twitter测试约20%），但是能够提高整个系统的HA也是相当划算的。不熟悉twemproxy的同学，如果玩过nginx反向代理或者MySQL proxy，那么你肯定也懂twemproxy了。其实twemproxy不光实现了Redis协议


### [2、写出如下代码的输出结果](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#2写出如下代码的输出结果)  


```python
def decorator_a(func):
print('Get in decorator_a')
def inner_a(*args, **kwargs):
print('Get in inner_a')
return func(*args, **kwargs)
return inner_a

def decorator_b(func):
print('Get in decorator_b')
def inner_b(*args, **kwargs):
print('Get in inner_b')
return func(*args, **kwargs)
return inner_b

@decorator_b #f=decorator_b(f)
@decorator_a #f=decorator_a(f)
def f(x):
print('Get in f')
return x 2
f(1)
```

答案

> Get in decorator_a

Get in decorator_b

Get in inner_b

Get in inner_a

Get in f


解释

> 当我们对f传入参数1进行调用时，inner_b被调用了，他会先打印Get in inner_b,然后在inner_b内部调用了inner_a,所以会再打印Get in inner_a,然后再inner_a内部调用原来的f,并且将结果作为最终的返回总结：装饰器函数在被装饰函数定义好后立即执行从下往上执行函数调用时从上到下执行



### [3、如何使用python删除一个文件或者文件夹？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#3如何使用python删除一个文件或者文件夹)  


```python
import os
import shutil
os.remove(path) # 删除文件
os.removedirs(path) # 删除空文件夹
shutil.rmtree(path) # 删除文件夹，可以为空也可以不为空
```


### [4、为什么学python](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#4为什么学python)  


答题路线：a、python的优点，b、python的应用领域广

**具体：**

优点

**1、** python语法非常优雅，简单易学

**2、** 免费开源

**3、** 跨平台，可以自由移植

**4、** 可扩展，可嵌入性强

**5、** 第三方库丰富

**应用领域**

**1、** 在系统编程中应用广泛，比如说shell工具。

**2、** 在网络爬虫方面功能非常强大，常用的库如scrapy，request等

**3、** 在web开发中使用也很广泛，如很多大型网站都用python开发的，如ins，youtube等，常用的框架如django，flask等

**4、** python在系统运维中应用广泛，尤其在linux运维方面，基本上都是自动化运维。

**5、** 在人工智能，云计算，金融等方面也应用非常广泛。


### [5、如何修改本地hosts文件](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#5如何修改本地hosts文件)  


进入c:\windows\system32\drivers\etc进行修改


### [6、编写程序，查找文本文件中最长的单词](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#6编写程序查找文本文件中最长的单词)  


```
def longest_word(filename):
    with open(filename, 'r') as infile:
              words = infile.read().split()
    max_len = len(max(words, key=len))
    return [word for word in words if len(word) == max_len]

print(longest_word('test.txt'))
----------------------------------------------------
['comprehensions']
```


### [7、用一行代码实现数值交换](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#7用一行代码实现数值交换)  


**1、** a=1

**2、** b=2

**3、** 答案：a,b=b,a


### [8、数据库的导入与导出命令](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#8数据库的导入与导出命令)  


**1、** 导出(MySQLdump)

**2、** 导出数据和表结构

**3、** MySQLdump -uroot -p dbname > dbname .sql

**4、** 只导出表结构

**5、** MySQLdump -uroot -p -d dbname > dbname .sql

6、导入

**7、** MySQL -u用户名 -p密码 数据库名 < 数据库名.sql


### [9、Redis中watch的作用](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#9redis中watch的作用)  


**1、** watch 用于在进行事务操作的最后一步也就是在执行exec 之前对某个key进行监视

**2、** 如果这个被监视的key被改动，那么事务就被取消，否则事务正常执行.

**3、** 一般在MULTI 命令前就用watch命令对某个key进行监控.如果想让key取消被监控，可以用unwatch命令


### [10、MySQL常见数据库引擎及区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题，高级面试题及附答案解析.md#10mysql常见数据库引擎及区别)  


**1、** InnoDB：用于事务处理应用程序，具有众多特性，包括ACID事务支持。(提供行级锁)

**2、** MyISAM：默认的MySQL插件式存储引擎，它是在Web、数据仓储和其他应用环境下最常使用的存储引擎之一。注意，通过更改STORAGE_ENGINE配置变量，能够方便地更改MySQL服务器的默认存储引擎。

**3、** Memory：将所有数据保存再RAM中


### 11、求以下代码结果：
### 12、有两个字符串列表a和b，每个字符串是由逗号隔开的一些字符
### 13、怎样获取字典中所有键的列表？
### 14、解释Python的内置数据结构？
### 15、三元运算编写格式
### 16、列表推导式[i for i in range(10)]和生成式表达式(i for i in range(10))的区别
### 17、什么是局域网和广域网
### 18、描述以下dict的items和iteritems的区别
### 19、为何不建议以下划线作为标识符的开头
### 20、如何打乱一个排好序的列表
### 21、什么是多态？
### 22、threading.local的作用
### 23、vuex的作用
### 24、or 和 and
### 25、解释Python中map()函数？
### 26、通过什么途径学习python
### 27、对字典d={'a':30,'g':17,'b':25,'c':18,'d':50,'e':36,'f':57,'h':25}按照value字段进行排序
### 28、lambda表达式格式以及应用场景？
### 29、为什么数据很大的时候使用limit offset分页时，越往后翻速度越慢，如何优化？
### 30、IO多路复用的作用？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




