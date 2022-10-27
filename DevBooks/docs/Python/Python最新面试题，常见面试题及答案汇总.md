# Python最新面试题，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是闭包](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#1什么是闭包)  


在函数中可以（嵌套）定义另一个函数时，如果内部的函数引用了外部的函数的变量，则可能产生闭包。闭包可以用来在一个函数与一组“私有”变量之间创建关联关系。在给定函数被多次调用的过程中，这些私有变量能够保持其持久性。

```python
# 内部函数使用了外部函数的变量，就相当于闭包
def func1():
a=1
def inner():
return a
return inner
print(func1()())
```


### [2、索引再什么情况下遵循最左前缀的规则？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#2索引再什么情况下遵循最左前缀的规则)  


在多字段进行索引的时候，会遵循以上原则


### [3、如何实现Redis集群](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#3如何实现redis集群)  


**1、** Twitter开发的twemproxy

**2、** 豌豆荚开发的codis

**3、** Redis官方的Redis-cluster


### [4、请列举布尔值位False的常见值](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#4请列举布尔值位false的常见值)  


0、''、[]、{}、tuple()、None、set()


### [5、什么是rpc](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#5什么是rpc)  


远程过程调用 (RPC) 是一种协议，程序可使用这种协议向网络中的另一台计算机上的程序请求服务

1.RPC采用客户机/服务器模式。请求程序就是一个客户机，而服务提供程序就是一个服务器。

2.首先，客户机调用进程发送一个有进程参数的调用信息到服务进程，然后等待应答信息。

2.在服务器端，进程保持睡眠状态直到调用信息到达为止。当一个调用信息到达，服务器获得进程参数，计算结果，发送答复信息，然后等待下一个调用信息，

3.最后，客户端调用进程接收答复信息，获得进程结果，然后调用执行继续进行。


### [6、a=range(10),则a[::-3]的值是？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#6a=range10,则a[::-3]的值是)  


[9,6,3,0] 或者 range(9,-1,-3)


### [7、写出邮箱的正则表达式](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#7写出邮箱的正则表达式)  


```python
import re
pp=re.compile('[a-zA-Z0-9_-]+@[0-9A-Za-z]+(\.[0-9a-zA-Z]+)+')
if pp.match('1403179190@qq.com'):
print('ok')
```


### [8、在Python中如何使用多进制数字？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#8在python中如何使用多进制数字)  


我们在Python中，除十进制外还可以使用二进制、八进制和十六进制。

**1、**   二进制数字由0和1组成，我们使用 0b 或 0B 前缀表示二进制数。

```
>>> int(0b1010)
10
```

**2、** 使用bin()函数将一个数字转换为它的二进制形式。

```
>>> bin(0xf)
‘0b1111’
```

**3、** 八进制数由数字 0-7 组成，用前缀 0o 或 0O 表示 8 进制数。

```
>>> oct(8)
‘0o10’
```

**4、** 十六进数由数字 0-15 组成，用前缀 0x 或者 0X 表示 16 进制数。

```
>>> hex(16)
‘0x10’
 
>>> hex(15)
‘0xf’
```


### [9、编写程序，输出给定序列中的所有质数](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#9编写程序输出给定序列中的所有质数)  


```
lower = int(input("Enter the lower range:"))
upper = int(input("Enter the upper range:"))
list(filter(lambda x:all(x % y != 0 for y in range(2, x)), range(lower, upper)))

-------------------------------------------------
Enter the lower range:10
Enter the upper range:50
[11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]
```


### [10、如何实现字符串的反转？如：name=felix，反转成name=xilef](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新面试题，常见面试题及答案汇总.md#10如何实现字符串的反转如：name=felix反转成name=xilef)  


```python
name = "felix"
# 方法一：
name=name[::-1]
# 方法二：
name2=list(name)
name2.reverse()
name=''.join(name2)
# 方法三：
from functools import reduce
name=reduce(lambda x, y: y+x, name)
```


### 11、写出以下代码的输出结果：
### 12、求以下代码的输出结果
### 13、什么是鸭子模型？
### 14、什么是防火墙？防火墙的作用是什么？
### 15、1，2，3，4，5能组成多少个互不相同且不重复的三位数？
### 16、super的作用
### 17、解释一下Python中的关系运算符
### 18、有如下链表类，请实现单链表逆置。
### 19、使用生成器编写一个函数实现生成指定个数的斐波那契数列
### 20、守护线程，守护进程是什么
### 21、什么是正则的贪婪匹配？贪婪模式和非贪婪模式的区别？
### 22、如何判断一个对象是否可调用？哪些对象是可调用对象？如何定义一个类，使其对象本身就是可调用对象？
### 23、前后端分离的基本原理
### 24、mro是什么？
### 25、一行代码通过filter和lambda函数输出alist=[1,22,2,33,23,32]中索引为奇数的值
### 26、写代码：如何由tuple1=('a','b','c','d','e')，和tuple2=(1,2,3,4,5)得到res={'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}
### 27、b、B、kB、MB、GB的关系
### 28、如何保证api调用时数据的安全性
### 29、解释什么是异步非阻塞
### 30、filter、map、reduce的作用。





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




