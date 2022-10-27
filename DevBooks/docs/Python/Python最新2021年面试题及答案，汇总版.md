# Python最新2022年面试题及答案，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Redis中默认有多少个哈希槽](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#1redis中默认有多少个哈希槽)  


**1、** 2^14个

**2、** Redis 集群没有使用一致性hash, 而是引入了哈希槽的概念。


### [2、实例变量和类变量的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#2实例变量和类变量的区别)  


**1、** 实例变量是对于每个实例都独有的数据

**2、** 类变量是该类所有实例共享的属性和方法


### [3、解释一下Python中的身份运算符](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#3解释一下python中的身份运算符)  


这也是一个在Python面试中常问的问题。

通过身份运算符‘is’和‘is not’，我们可以确认两个值是否相同。

```
>>> 10 is '10'
False
 
>>> True is not False
True
```


### [4、yield from 和 yield 的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#4yield-from-和-yield-的区别)  


[简述yield和yield from](https://blog.csdn.net/lamusique/article/details/85845225)

```python
# 下面a()和b()是等价的
def a():
yield from [1,2,3,4,5]
def b():
for i in [1,2,3,4,5]:
yield i
for i in a():
print(i)
for i in b():
print(i)
```

yield将一个函数变成一个生成器

yield 返回一个值

yield from后面接可迭代对象，一个一个返回值。


### [5、py2项目如何迁移成py3](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#5py2项目如何迁移成py3)  


**1、** 先备份原文件，然后使用python3自带工具2to3.py将py2文件转换位py3文件

**2、** 手动将不兼容的代码改写成兼容py3的代码


### [6、生产者消费者模型的应用场景](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#6生产者消费者模型的应用场景)  


**说明**

生产者只在仓库未满时进行生产，仓库满时生产者进程被阻塞；消费者只在仓库非空时进行消费，仓库为空时消费者进程被阻塞；

应用场景：处理数据比较消耗时间，线程独占，生产数据不需要即时的反馈等。比如说写入日志，将多线程产生的日志放在队列中，然后写入。


### [7、简述数据库的读写分离](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#7简述数据库的读写分离)  


读写分离就是在主服务器上修改，数据会同步到从服务器，从服务器只能提供读取数据，不能写入，实现备份的同时也实现了数据库性能的优化，以及提升了服务器安全。


### [8、解释//、％、* *运算符？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#8解释//％*-*运算符)  


//(Floor Division)-这是一个除法运算符，它返回除法的整数部分。

例如：5 // 2 = 2

％(模数)-返回除法的余数。

例如：5 ％ 2 = 1

**(幂)-它对运算符执行指数计算。a ** b表示a的b次方。

例如：5 ** 2 = 25、5 ** 3 = 125


### [9、什么是轮询和长轮询](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#9什么是轮询和长轮询)  


轮询是在特定的的时间间隔（如每1秒），由浏览器对服务器发出HTTP request，然后由服务器返回最新的数据给客户端的浏览器。这种传统的HTTP request 的模式带来很明显的缺点 – 浏览器需要不断的向服务器发出请求，然而HTTP request 的header是非常长的，里面包含的有用数据可能只是一个很小的值，这样会占用很多的带宽。

```javascript
var xhr = new XMLHttpRequest();
setInterval(function() {
    xhr.open('GET', '/user');
    xhr.onreadystatechange = function() {};
    xhr.send();
}, 1000)
```

长轮询是ajax实现:在发送ajax后,服务器端会阻塞请求直到有数据传递或超时才返回。 客户端JavaScript响应处理函数会在处理完服务器返回的信息后，再次发出请求，重新建立连接。

```javascript
function ajax() {
    var xhr = new XMLHttpRequest();
    xhr.open('GET', '/user');
    xhr.onreadystatechange = function() {
        ajax();
    };
    xhr.send();
}
```


### [10、如果Redis中的某个列表中的数据量非常大，如何实现循环显示每一个值？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题及答案，汇总版.md#10如果redis中的某个列表中的数据量非常大如何实现循环显示每一个值)  


使用生成器一个一个取


### 11、简述生成器，迭代器，装饰器以及应用场景
### 12、比较：a=[1,2,3]和b=[(1),(2),(3)]以及c=[(1,),(2,),(3,)]的区别
### 13、什么是c3算法？
### 14、字节码和机器码的区别
### 15、MySQL执行计划的作用和使用方法
### 16、简述left join和right join的区别
### 17、什么是LVS
### 18、求下面代码结果
### 19、python中enumerate的意思是什么？
### 20、常用字符串格式化有哪几种？
### 21、列举字符串、列表、元组、字典每个常用的5个方法
### 22、如何更改列表的数据类型？
### 23、什么是一致性哈希
### 24、曾经使用过哪些前端框架
### 25、简述OSI七层协议
### 26、python递归的最大层数？
### 27、如何用一行代码生成[1,4,9,16,25,36,49,64,81,100]?
### 28、query作为sql模板，args为将要传入的参数
### 29、使用with语句的好处是什么
### 30、什么是lambda函数？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




