# Python最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、解释re模块的split()、sub()、subn()方法？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#1解释re模块的splitsubsubn方法)  


split()：只要模式匹配，此方法就会拆分字符串。

sub()：此方法用于将字符串中的某些模式替换为其他字符串或序列。

subn()：和sub()很相似，不同之处在于它返回一个元组，将总替换计数和新字符串作为输出。

```
import re
string = "There are two ball in the basket 101"


re.split("\W+",string)
---------------------------------------
['There', 'are', 'two', 'ball', 'in', 'the', 'basket', '101']

re.sub("[^A-Za-z]"," ",string)
----------------------------------------
'There are two ball in the basket'

re.subn("[^A-Za-z]"," ",string)
-----------------------------------------
('There are two ball in the basket', 10)
```


### [2、简述面向对象的三大特性？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#2简述面向对象的三大特性)  


继承，封装和多态

**继承：**

继承就是继承的类直接拥有被继承类的属性而不需要在自己的类体中重新再写一遍，其中被继承的类叫做父类、基类，继承的类叫做派生类、子类。

**封装：**

封装就是把类中的属性和方法定义为私有的，方法就是在属性名或方法名前加双下划线，而一旦这样定义了属性或方法名后，python会自动将其转换为_类名**属性名（方法名）的格式，在类的内部调用还是用双下划线加属性名或方法名，在类的外部调用就要用**类名_属性名（方法名）。父类的私有属性和方法，子类无法对其进行修改。

**多态：**

多态就是不同的对象可以调用相同的方法然后得到不同的结果，有点类似接口类的感觉，在python中处处体现着多态，比如不管你是列表还是字符串还是数字都可以使用+和*。


### [3、是否使用过functools中的函数？他的作用是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#3是否使用过functools中的函数他的作用是什么)  


**1、** functools.wraps()

在装饰器中用过，如果不使用wraps，则原始函数的**name**和**doc**的值就会丢失

**2、** functools.reduce()

第一个参数是一个函数，第二个参数是一个可迭代对象，代码如下：

```python
# 下面代码相当于从1加到9
from functools import reduce
a=reduce(lambda x,y:x+y,range(10))
print(a)
```


### [4、Redis和Memcached的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#4redis和memcached的区别)  


**1、** 存储方式：

Memecache把数据全部存在内存之中，断电后会挂掉，数据不能超过内存大小。Redis有部份存在硬盘上，这样能保证数据的持久性。

**2、** 数据支持类型

Memcache对数据类型支持相对简单。Redis有复杂的数据类型。

**3、** 使用底层模型不同

它们之间底层实现方式 以及与客户端之间通信的应用协议不一样。Redis直接自己构建了VM 机制 ，因为一般的系统调用系统函数的话，会浪费一定的时间去移动和请求。

**4、** value大小

Redis最大可以达到1GB，而memcache只有1MB


### [5、简述进程，线程，协程的区别以及应用场景？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#5简述进程线程协程的区别以及应用场景)  


**区别：**

**1、** 线程是资源分配的单位

**2、** 线程是操作系统调度的单位

**3、** 进程切换需要的资源很大，效率很低

**4、** 线程切换需要的资源一般，效率一般(在不考虑GIL的情况下

**5、** 协程切换任务资源很小，效率高

**6、** 多进程，多线程根据cpu核数不一样可能是并行的，但是协程是在一个线程中，所以是并发。)

**应用场景**

**1、** 协程：当程序中存在大量不需要cpu的操作时，适用协程

**2、** 计算密集型，用进程。IO密集型，用线程。


### [6、_init_在Python中有什么用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#6_init_在python中有什么用)  


“__init__”是Python类中的保留方法。

它被称为构造函数，每当执行代码时都会自动调用它，它主要用于初始化类的所有变量。


### [7、什么是正向代理和反向代理？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#7什么是正向代理和反向代理)  


**正向代理**

**1、** 正向代理类似一个跳板机，代理访问外部资源。

**2、** 正向代理 是一个位于客户端和原始服务器(origin server)之间的服务器，为了从原始服务器取得内容，客户端向代理发送一个请求并指定目标(原始服务器)，然后代理向原始服务器转交请求并将获得的内容返回给客户端。客户端必须要进行一些特别的设置才能使用正向代理。

**正向代理作用：**

**1、** 访问原来无法访问的资源，如google

**2、** 可以做缓存，加速访问资源

**3、** 对客户端访问授权，上网进行认证

**4、** 代理可以记录用户访问记录（上网行为管理），对外隐藏用户信息

**反向代理**

**1、** 反向代理（Reverse Proxy）实际运行方式是指以代理服务器来接受internet上的连接请求，然后将请求转发给内部网络上的服务器，并将从服务器上得到的结果返回给internet上请求连接的客户端，此时代理服务器对外就表现为一个服务器

**反向代理的作用：**

**1、** 保证内网的安全，可以使用反向代理提供WAF功能，阻止web攻击

**2、** 负载均衡，通过反向代理服务器来优化网站的负载


### [8、怎样声明多个变量并赋值？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#8怎样声明多个变量并赋值)  


一共有两种方式：

```
>>> a,b,c=3,4,5 #This assigns 3, 4, and 5 to a, b, and c respectively
>>> a=b=c=3 #This assigns 3 to a, b, and c
```


### [9、请列举你所知道的python代码检测工具以及他们之间的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#9请列举你所知道的python代码检测工具以及他们之间的区别)  


**1、** pylint --- 源代码分析器，可以分析python代码中的错误

**2、** pyflakes --- 检查源文件错误的简单程序，不会检查代码风格。

**3、** pep8 --- 检查代码规范的工具


### [10、简述Redis的有几种持久化策略以及比较？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题及答案附答案汇总.md#10简述redis的有几种持久化策略以及比较)  


**1、** RDB 持久化可以在指定的时间间隔内生成数据集的时间点快照。

**2、** AOF 持久化记录服务器执行的所有写操作命令，并在服务器启动时，通过重新执行这些命令来还原数据集。 AOF 文件中的命令全部以 Redis 协议的格式来保存，新命令会被追加到文件的末尾。 Redis 还可以在后台对 AOF 文件进行重写(rewrite)，使得 AOF 文件的体积不会超出保存数据集状态所需的实际大小。

**区别：**

**1、** RDB持久化是指在指定的时间间隔内将内存中的数据集快照写入磁盘，实际操作过程是fork一个子进程，先将数据集写入临时文件，写入成功后，再替换之前的文件，用二进制压缩存储。

**2、** AOF持久化以日志的形式记录服务器所处理的每一个写、删除操作，查询操作不会记录，以文本的方式记录，可以打开文件看到详细的操作记录。


### 11、使用两个队列实现一个栈
### 12、用一行Python代码，从给定列表中取出所有的偶数和奇数
### 13、Python中的标识符长度能有多长？
### 14、MySQL的半同步复制原理
### 15、Python中注释代码的方法有哪些？
### 16、使用async语法实现一个协程
### 17、请解释使用*args和**kwargs的含义
### 18、写一个的支持with语句的类
### 19、编写一个函数，找出数组中没有重复的值的和
### 20、简述解释型和编译型编程语言
### 21、位和字节的关系
### 22、下面代码的执行结果是
### 23、有一个列表lis=['This','is','a','Man','B','!']，对它进行大小写无关的排序
### 24、Python支持多重继承吗？
### 25、如何查找一个字符串中特定的字符？find和index的差异？
### 26、简述TCP三次握手，四次挥手的流程。
### 27、Python中的装饰器是什么？
### 28、xrange和range的区别
### 29、python的可变类型和不可变类型的区别
### 30、什么是粘包？出现粘包的原因？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




