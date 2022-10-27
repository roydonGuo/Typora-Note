# Python最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、break、continue、pass是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#1breakcontinuepass是什么)  


break：在满足条件时，它将导致程序退出循环。

continue：将返回到循环的开头，它使程序在当前循环迭代中的跳过所有剩余语句。

pass：使程序传递所有剩余语句而不执行。


### [2、ascii、Unicode、utf-8、gbk的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#2asciiunicodeutf-8gbk的区别)  


**1、** ascii 是最早美国用的标准信息交换码，把所有的字母的大小写，各种符号用 二进制来表示，共有256中，加入些拉丁文等字符，1bytes代表一个字符

**2、** Unicode是为了统一世界各国语言的不用，统一用2个bytes代表一个字符，可以表达2^16=65556个，称为万国语言，特点：速度快，但浪费空间

**3、** utf-8 为了改变Unicode的这种缺点，规定1个英文字符用1个字节表示，1个中文字符用3个字节表示，特点；节省空间，速度慢，用在硬盘数据传输，网络数据传输，相比硬盘和网络速度，体现不出来的

**4、** gbk  是中文的字符编码，用2个字节代表一个字符


### [3、如何在Python中管理内存？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#3如何在python中管理内存)  


Python内存由Python的私有headspace管理。

所有的Python对象和数据结构都位于一个私有堆中。私用堆的分配由Python内存管理器负责。

Python还内置了一个的垃圾收集器，可以回收未使用的内存并释放内存，使其可用于headspace。


### [4、Python中的Map Function是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#4python中的map-function是什么)  


map函数在对可迭代对象的每一项应用特定函数后，会返回map对象。


### [5、如何保证Redis中的数据都是热点数据](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#5如何保证redis中的数据都是热点数据)  


**1、** Redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。Redis 提供 6种数据淘汰策略：

**2、** volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰

**3、** volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰

**4、** volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰

**5、** allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰

**6、** allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰

**7、** no-enviction（驱逐）：禁止驱逐数据


### [6、当退出Python时，是否释放全部内存？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#6当退出python时是否释放全部内存)  


答案是No。循环引用其它对象或引用自全局命名空间的对象的模块，在Python退出时并非完全释放。

另外，也不会释放C库保留的内存部分。


### [7、select、poll、epoll模型的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#7selectpollepoll模型的区别)  


**1、** 支持一个进程所能打开的最大连接数

select的最大连接数大概32_32，或者32_64

poll本质和select没区别，但是它没有最大连接数限制

epoll大概10万左右(1G的机器)

**2、** FD剧增后带来的IO效率问题

select和poll每次调用都会对连接进行线性遍历，所以会随着FD的增加会造成遍历速度慢的“线性下降性能问题”

epoll没有前两个的线性下降的性能问题，但是当socket都很活跃的情况下，可能会有性能问题。

**3、** 消息传递方式

select和poll内核需要将消息传递到用户空间，都需要内核拷贝动作。

epoll通过内核和用户空间共享一块内存来实现


### [8、什么是C/S和B/S架构](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#8什么是c/s和b/s架构)  


**1、** C/S 架构是一种典型的两层架构，其全称是Client/Server，即客户端服务器端架构，其客户端包含一个或多个在用户的电脑上运行的程序，而服务器端有两种，一种是数据库服务器端，客户端通过数据库连接访问服务器端的数据；另一种是Socket服务器端，服务器端的程序通过Socket与客户端的程序通信。

**2、** B/S架构的全称为Browser/Server，即浏览器/服务器结构。Browser指的是Web浏览器，极少数事务逻辑在前端实现，但主要事务逻辑在服务器端实现，Browser客户端，WebApp服务器端和DB端构成所谓的三层架构。B/S架构的系统无须特别安装，只有Web浏览器即可。


### [9、列举Redis支持的过期策略](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#9列举redis支持的过期策略)  


**定时删除**

在设置key的过期时间的同时，为该key创建一个定时器，让定时器在key的过期时间来临时，对key进行删除

**惰性删除**

key过期的时候不删除，每次从数据库获取key的时候去检查是否过期，若过期，则删除，返回null。

**定期删除**

每隔一段时间执行一次删除(在Redis.conf配置文件设置hz，1s刷新的频率)过期key操作


### [10、输入某年某月某日，判断这是这一年的第几天？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题附答案解析，大汇总.md#10输入某年某月某日判断这是这一年的第几天)  


```python
date=input('请输入某年某月某日，格式：xxxx.xx.xx')
def get_day(date):
days1=[31,28,31,30,31,30,31,31,30,31,30,31]
days2=[31,29,31,30,31,30,31,31,30,31,30,31]
year,month,day = [int(i) for i in date.split('.')]
if year % 400 ==0 or (year % 4==0 and year % 100!=0):
days=days2
else:
days=days1
return sum(days[:month-1])+day
print(get_day(date))
```


### 11、列表和元组之间的区别是？
### 12、DNS域名解析过程
### 13、什么是猴子补丁？
### 14、在Python中是如何管理内存的？
### 15、Python有什么特点？
### 16、解释一下Python中的逻辑运算符
### 17、==和is的区别是？
### 18、Python中的闭包是什么？
### 19、Python中使用的zip函数是什么？
### 20、元组的解封装是什么？
### 21、什么是Python？为什么它会如此流行？
### 22、logging模块的作用以及应用场景
### 23、为什么基于tcp协议的通信比基于udp协议的通信更可靠
### 24、将下面列表中的元素根据位数合并成字典：
### 25、关于Python程序的运行方面，有什么手段能提升性能？
### 26、双下划线和单下划线的区别
### 27、什么是arp协议
### 28、Redis中sentinel的作用
### 29、以下代码输出什么？
### 30、进程之间如何进行通信？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




