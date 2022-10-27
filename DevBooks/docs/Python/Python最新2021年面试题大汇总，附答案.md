# Python最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Python的局限性？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#1python的局限性)  


**1、**  速度

**2、**  移动开发

**3、**  内存消耗(与其他语言相比非常高)

**4、**  两个版本的不兼容(2，3)

**5、**  运行错误(需要更多测试，并且错误仅在运行时显示)

**6、**  简单性


### [2、区分Python中的remove，del和pop？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#2区分python中的removedel和pop)  


remove：将删除列表中的第一个匹配值，它以值作为参数。

del：使用索引删除元素，它不返回任何值。

pop：将删除列表中顶部的元素，并返回列表的顶部元素。

```
numbers = [1,2,3,4,5]
numbers.remove(5)
> [1,2,3,4]

del numbers[0]
>[2,3,4]

numbers.pop()
>4
```


### [3、什么是ajax请求？手写一个ajax请求](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#3什么是ajax请求手写一个ajax请求)  


ajax（异步JavaScript和XML）是指一种创建交付式网页应用的网页开发技术。可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

```javascript
// 不使用第三方
var xhr = new XMLHttpRequest();
xhr.open("GET", url, false);
xhr.onreadtstatechange = function() {
    if (xhr.readystate == 4) {
        //响应内容解析完成，可以在客户端调用了
        if (xhr.status == 200) {
            //客户端的请求成功了
            alert(xhr.responseText);
        }
    }
}
xhr.send(null);
// 使用ajax
$.ajax({
    type: "GET",
    url: "",
    dataType: "json",
    success: function(data) {},
    error: function(jqXHR) {}
});
```


### [4、什么是覆盖索引](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#4什么是覆盖索引)  


**覆盖索引又可以称为索引覆盖。**

**1、** 解释一： 就是select的数据列只用从索引中就能够取得，不必从数据表中读取，换句话说查询列要被所使用的索引覆盖。

**2、** 解释二： 索引是高效找到行的一个方法，当能通过检索索引就可以读取想要的数据，那就不需要再到数据表中读取行了。如果一个索引包含了（或覆盖了）满足查询语句中字段与条件的数据就叫做覆盖索引。

**3、** 解释三： 是非聚集组合索引的一种形式，它包括在查询里的Select、Join和Where子句用到的所有列（即建立索引的字段正好是覆盖查询语句[select子句]与查询条件[Where子句]中所涉及的字段，也即，索引包含了查询正在查找的所有数据）。


### [5、简述多进程开发中join和deamon的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#5简述多进程开发中join和deamon的区别)  


**1、** join：当子线程调用join时，主线程会被阻塞，当子线程结束后，主线程才能继续执行。

**2、** deamon：当子进程被设置为守护进程时，主进程结束，不管子进程是否执行完毕，都会随着主进程的结束而结束。


### [6、在Python中有多少种运算符？解释一下算数运算符。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#6在python中有多少种运算符解释一下算数运算符。)  


在Python中，我们有7种运算符：算术运算符、关系运算符、赋值运算符、逻辑运算符、位运算符、成员运算符、身份运算符。

我们有7个算术运算符，能让我们对数值进行算术运算：

**1、** 加号（+），将两个值相加

```
>>> 7+8
15
```

**2、** 减号（-），将第一个值减去第二个值

```
>>> 7-8
-1
```

**3、** 乘号（*），将两个值相乘

```
>>> 7*8
56
```

**4、** 除号（/），用第二个值除以第一个值

```
>>> 7/8
0.875
>>> 1/1
1.0
```

**5、** 向下取整除、取模和取幂运算，参见上个问题。


### [7、python3和python2中int和long的区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#7python3和python2中int和long的区别)  


python2中有long类型，python3中没有long类型，只有int类型。python3中的int类型包括了long类型。


### [8、什么是抽象？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#8什么是抽象)  


抽象(Abstraction)是将一个对象的本质或必要特征向外界展示，并隐藏所有其他无关信息的过程。


### [9、将列表alist=[{'name':'a','age':25},{'name':'b','age':30},{'name':'c','age':20}]，按照age的值从大到小排列。](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#9将列表alist=[{'name':'a','age':25},{'name':'b','age':30},{'name':'c','age':20}]按照age的值从大到小排列。)  


```python
alist=[{'name':'a','age':25},{'name':'b','age':30},{'name':'c','age':20}]
blist=sorted(alist,key=lambda x:x['age'],reverse=True)
print(blist)
```


### [10、解释一下Python中的继承](https://gitee.com/souyunku/DevBooks/blob/master/docs/Python/Python最新2021年面试题大汇总，附答案.md#10解释一下python中的继承)  


当一个类继承自另一个类，它就被称为一个子类/派生类，继承自父类/基类/超类。它会继承/获取所有类成员（属性和方法）。

继承能让我们重新使用代码，也能更容易的创建和维护应用。Python支持如下种类的继承：

- 单继承：一个类继承自单个基类
- 多继承：一个类继承自多个基类
- 多级继承：一个类继承自单个基类，后者则继承自另一个基类
- 分层继承：多个类继承自单个基类
- 混合继承：两种或多种类型继承的混合 更多关于继承的内容，参见：

[戳这里](https://data-flair.training/blogs/python-inheritance/)


### 11、解释一下Python中的三元运算子
### 12、什么是Nginx
### 13、!=和is not运算符的区别？
### 14、介绍一下try except的用法和作用？
### 15、公司线上和开发环境使用的什么系统
### 16、什么是keepalived
### 17、如何使用索引来反转Python中的字符串?
### 18、从0-99这100个数中随机取出10个，要求不能重复
### 19、实例方法、静态方法和类方法的区别
### 20、什么是gevent
### 21、python是如何进行内存管理的？python的程序会内存泄漏吗？说说有没有什么方面阻止或者检测内存泄漏？
### 22、请写一个Python逻辑，计算一个文件中的大写字母数量
### 23、获取python解释器版本的方法
### 24、什么是负载均衡
### 25、类的加载和实例化过程
### 26、路由器和交换机的区别
### 27、Python中的生成器是什么？
### 28、索引有什么作用，有哪些分类，有什么好处和坏处？
### 29、1<(22)和1<22的结果分别是什么？
### 30、什么是域名解析





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




