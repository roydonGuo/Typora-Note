# JavaScript最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、JavaScript提供了哪几种“异步模式”？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#1javascript提供了哪几种“异步模式)  


**1、** 回调函数（callbacks）

**2、** 事件监听

**3、** Promise对象


### [2、sessionStorage和localstroage与cookie之间有什么关联, cookie最大存放多少字节](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#2sessionstorage和localstroage与cookie之间有什么关联,-cookie最大存放多少字节)  


**三者共同点：**

都是保存在浏览器端，且同源的。

区别:

**1、** cookie在浏览器和服务器间来回传递。而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存

**2、** 存储大小限制也不同，cookie数据不能超过4k，sessionStorage和localStorage 但比cookie大得多，可以达到5M

**3、** 数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持；localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭

**4、** 作用域不同，sessionStorage不在不同的浏览器窗口中共享，即使是同一个页面(即数据不共享)；localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的( 即数据共享 )。


### [3、new操作符具体干了什么呢?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#3new操作符具体干了什么呢)  


**1、** 创建一个空对象，并且 `this` 变量引用该对象，同时还继承了该函数的原型

**2、** 属性和方法被加入到 `this` 引用的对象中

**3、** 新创建的对象由 `this` 所引用，并且最后隐式的返回 `this`


### [4、sass和less有什么区别?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#4sass和less有什么区别)  


**1、** 编译环境不一样 Sass的安装需要Ruby环境，是在服务端处理的，而Less是需要引入less.js来处理Less代码输出css到浏览器，也可以在开发环节使用Less，然后编译成css文件，直接放到项目中。

**2、** 变量符不一相，less是@，而scss是$,而且它们的作用域也不一样，less是块级作用域

**3、** 输出设置，Less没有输出设置，sass提供4种输出选项，nested,compact,compressed和expanded nested：嵌套缩进的css代码(默认) expanded：展开的多行css代码 compact：简洁格式的css代码 compressed：压缩后的css代码

**4、** sass支持条件语句，可以使用if{}else{},for{}循环等等，而less不行

**5、** 引用外部css文件，sass引用外部文件必须以_开头，文件名如果以下划线_形状，sass会认为该文件是一个引用文件，不会将其编译为css文件。less引用外部文件和css中的@import没什么差异。

**6、** sass和less的工具库不同。sass有工具库Compass, 简单说，sass和Compass的关系有点像Javascript和jQuery的关系,Compass是sass的工具库。在它的基础上，封装了一系列有用的模块和模板，补充强化了sass的功能。less有UI组件库Bootstrap,Bootstrap是web前端开发中一个比较有名的前端UI组件库，Bootstrap的样式文件部分源码就是采用less语法编写。

总结：不管是sass，还是less，都可以视为一种基于CSS之上的高级语言，其目的是使得CSS开发更灵活和更强大，sass的功能比less强大,基本可以说是一种真正的编程语言了，less则相对清晰明了,易于上手,对编译环境要求比较宽松。考虑到编译sass要安装Ruby,而Ruby官网在国内访问不了,个人在实际开发中更倾向于选择less。


### [5、谈谈This对象的理解](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#5谈谈this对象的理解)  


**1、** `this`总是指向函数的直接调用者（而非间接调用者）

**2、** 如果有`new`关键字，`this`指向`new`出来的那个对象

**3、** 在事件中，`this`指向触发这个事件的对象，特殊的是，`IE`中的`attachEvent`中的`this`总是指向全局对象`Window`


### [6、new 关键字有什么作用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#6new-关键字有什么作用)  


`new`关键字与构造函数一起使用以创建对象:

```
function Employee(name, position, yearHired) {
  this.name = name;
  this.position = position;
  this.yearHired = yearHired;
};

const emp = new Employee("Marko Polo", "Software Developer", 2017);
```

`new`关键字做了`4`件事:

**1、** 创建空对象 `{}`

**2、** 将空对象分配给 `this` 值

**3、** 将空对象的`__proto__`指向构造函数的`prototype`

**4、** 如果没有使用显式`return`语句，则返回`this`

看下面事例：

`function Person() { this.name = 'kyle' }`

根据上面描述的，`new Person()`做了：

**1、** 创建一个空对象：`var obj = {}`

**2、** 将空对象分配给 `this` 值：this = obj

**3、** 将空对象的`__proto__`指向构造函数的`prototype`:`this.__proto__ = Person().prototype`

**4、** 返回`this`:`return this`



### [7、数组的排序方法（sort）？排序？汉字排序？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#7数组的排序方法sort排序汉字排序)  


数组的排序方法：reverse()和sort()。reverse()方法会对反转数组项的顺序。

Eg:var values = [0, 1, 5, 10, 15]; values.sort();//0,1,10,15,5

var values = [1, 2, 3, 4, 5]; values.reverse();//5,4,3,2,1

js中的排序（详情参考： [http://www.tuicool.com/articles/IjInMbU](http://link.zhihu.com/?target=http%3A//www.tuicool.com/articles/IjInMbU)）

利用sort排序, 冒泡排序, 快速排序, 插入排序, 希尔排序, 选择排序

归并排序

localeCompare() 方法用于字符串编码的排序

localeCompare 方法：返回一个值，指出在当前的区域设置中两个字符串是否相同。


### [8、git 和 svn的区别?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#8git-和-svn的区别)  


SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话，就纳闷了。

Git是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库，这样，工作的时候就不需要联网了，因为版本都是在自己的电脑上。既然每个人的电脑都有一个完整的版本库，那多个人如何协作呢？比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。


### [9、如何改变this指针的指向？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#9如何改变this指针的指向)  


可以使用`apply`、`call`、`bind`方法改变`this`指向(并不会改变函数的作用域)。比较如下：

**1、** 三者第一个参数都是`this`要指向的对象，也就是想指定的上下文，上下文就是指调用函数的那个对象(没有就指向全局window)；

**2、** `bind`和`call`的第二个参数都是数组，`apply`接收多个参数并用逗号隔开；

**3、** `apply`和`call`只对原函数做改动，`bind`会返回新的函数(要生效还得再调用一次)。


### [10、如何合并两个数组？数组删除一个元素?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题附答案解析，大汇总.md#10如何合并两个数组数组删除一个元素)  


```
//三种方法。

（1）var arr1=[1,2,3];
        var arr2=[4,5,6];
        arr1 = arr1.concat(arr2);
        console.log(arr1); 
        
（2）var arr1=[1,2,3];
        var arr2=[4,5,6];
        Array.prototype.push.apply(arr1,arr2);
        console.log(arr1);
        
（3）var arr1=[1,2,3];
    var arr2=[4,5,6];
    for (var i=0; i < arr2.length; i++) {
    arr1.push( arr2[i] );
    }
    console.log(arr1);
```


### 11、如何创建一个没有 prototype(原型)的对象？
### 12、展开(spread )运算符和 剩余(Rest) 运算符有什么区别？
### 13、如何在 JS 中创建对象？
### 14、什么是默认参数？
### 15、Jq中如何将一个jq对象转化为dom对象？
### 16、什么是预编译语音|预编译处理器?
### 17、说说你对promise的了解
### 18、`var`,`let`和`const`的区别是什么？
### 19、手动实现`Array.prototype.filter`方法
### 20、什么是闭包? 堆栈溢出有什么区别？ 内存泄漏? 那些操作会造成内存泄漏？怎么样防止内存泄漏？
### 21、什么是闭包？
### 22、什么是 event.target ？
### 23、26.移动端上什么是点击穿透?
### 24、ES6或ECMAScript 2015有哪些新特性？
### 25、请解释什么是事件代理
### 26、slice() splice()?
### 27、什么是跨域？怎么解决跨域问题？
### 28、用过哪些设计模式？
### 29、!! 运算符能做什么？
### 30、除了jsonp 还有什么跨域方式###





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




