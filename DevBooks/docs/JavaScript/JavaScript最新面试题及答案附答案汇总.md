# JavaScript最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、模块化开发怎么做？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#1模块化开发怎么做)  


立即执行函数,不暴露私有成员

```
var module1 = (function(){
　　　　var _count = 0;
　　　　var m1 = function(){
　　　　　　//...
　　　　};
　　　　var m2 = function(){
　　　　　　//...
　　　　};
　　　　return {
　　　　　　m1 : m1,
　　　　　　m2 : m2
　　　　};
　　})();
```


### [2、vue、react、angular](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#2vuereactangular)  


**`Vue.js`**

一个用于创建 `web` 交互界面的库，是一个精简的 `MVVM`。它通过双向数据绑定把 `View` 层和 `Model` 层连接了起来。实际的 `DOM` 封装和输出格式都被抽象为了`Directives` 和 `Filters`

**`AngularJS`**

是一个比较完善的前端`MVVM`框架，包含模板，数据双向绑定，路由，模块化，服务，依赖注入等所有功能，模板功能强大丰富，自带了丰富的 `Angular`指令

**`react`**

`React` 仅仅是 `VIEW` 层是`facebook`公司。推出的一个用于构建`UI`的一个库，能够实现服务器端的渲染。用了`virtual dom`，所以性能很好。


### [3、什么是 `async/await` 及其如何工作？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#3什么是-async/await-及其如何工作)  


`async/await`是 JS 中编写异步或非阻塞代码的新方法。它建立在**Promises**之上，让异步代码的可读性和简洁度都更高。

`async/await`是 JS 中编写异步或非阻塞代码的新方法。它建立在`Promises`之上，相对于 Promise 和回调，它的可读性和简洁度都更高。但是，在使用此功能之前，我们必须先学习`Promises`的基础知识，因为正如我之前所说，它是基于`Promise`构建的，这意味着幕后使用仍然是**Promise**。

**使用 Promise**

```
function callApi() {
  return fetch("url/to/api/endpoint")
    .then(resp => resp.json())
    .then(data => {
      //do something with "data"
    }).catch(err => {
      //do something with "err"
    });
}
```

**使用async/await**

在`async/await`，我们使用 tru/catch 语法来捕获异常。

```
async function callApi() {
 try {
   const resp = await fetch("url/to/api/endpoint");
   const data = await resp.json();
   //do something with "data"
 } catch (e) {
   //do something with "err"
 }
}
```

**注意**:使用 `async`关键声明函数会隐式返回一个**Promise**。

```
const giveMeOne = async () => 1;
giveMeOne()
  .then((num) => {
    console.log(num); // logs 1
  });
```

**注意:**`await`关键字只能在`async function`中使用。在任何非**async function**的函数中使用`await`关键字都会抛出错误。`await`关键字在执行下一行代码之前等待右侧表达式(可能是一个**Promise**)返回。

```
const giveMeOne = async () => 1;

function getOne() {
  try {
    const num = await giveMeOne();
    console.log(num);
  } catch (e) {
    console.log(e);
  }
}

// Uncaught SyntaxError: await is only valid in async function

async function getTwo() {
  try {
    const num1 = await giveMeOne(); // 这行会等待右侧表达式执行完成
    const num2 = await giveMeOne(); 
    return num1 + num2;
  } catch (e) {
    console.log(e);
  }
}

await getTwo(); // 2
```


### [4、实现异步的方式有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#4实现异步的方式有哪些)  


**1、** 回调函数模式：将需要异步执行的函数作为回调函数执行，其缺点在于处理复杂逻辑异步逻辑时，会造成回调地狱(回调嵌套层数太多，代码结构混乱)；

**2、** 事件监听模式：采用事件驱动的思想，当某一事件发生时触发执行异步函数，其缺点在于整个代码全部得变为事件驱动模式，难以分辨主流程；

**3、** 发布订阅模式：当异步任务执行完成时发布消息给信号中心，其他任务通过在信号中心中订阅消息来确定自己是否开始执行；

**4、** Promise(ES6)：`Promise`对象共有三种状态`pending`(初始化状态)、`fulfilled`(成功状态)、`rejected`(失败状态)。

**5、** async/await(ES7)：基于`Promise`实现的异步函数； （6）利用生成器实现。


### [5、JavaScript有几种类型的值？，你能画一下他们的内存图吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#5javascript有几种类型的值你能画一下他们的内存图吗)  


**1、** 栈：原始数据类型（`Undefined`，`Null`，`Boolean`，`Numbe`r、`String`）

**2、** 堆：引用数据类型（对象、数组和函数）

**3、** 两种类型的区别是：存储位置不同；

**4、** 原始数据类型直接存储在栈(`stack`)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；

**5、** 引用数据类型存储在堆(`heap`)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其

**6、** 在栈中的地址，取得地址后从堆中获得实体

![33_1.png][33_1.png]


### [6、介绍js的基本数据类型](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#6介绍js的基本数据类型)  


`Undefined`、`Null`、`Boolean`、`Number`、`String`


### [7、eval是做什么的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#7eval是做什么的)  


**1、** 它的功能是把对应的字符串解析成`JS`代码并运行

**2、** 应该避免使用`eval`，不安全，非常耗性能（`2`次，一次解析成`js`语句，一次执行）

**3、** 由`JSON`字符串转换为JSON对象的时候可以用`eval，var obj =eval('('+ str +')')`


### [8、undefined 和 null 有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#8undefined-和-null-有什么区别)  


在理解 `undefined` 和 `null` 的差异之前，我们先来看看它们的相似点。

**它们都属于 JavaScript 的 7 种基本类型。**

```
let primitiveTypes = ['string','number','null','undefined','boolean','symbol', 'bigint'];
```

它们是属于 falsy 值类型，可以使用 `Boolean(value)` 或 `!!value` 将其转换为布尔值时，值为`false`。

```
console.log(!!null); // false
console.log(!!undefined); // false

console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
```

接着来看看它们的区别。

`undefined` 是未指定特定值的变量的默认值，或者没有显式返回值的函数，如：`console.log(1)`，还包括对象中不存在的属性，这些 JS 引擎都会为其分配 `undefined` 值。

```
let _thisIsUndefined;
const doNothing = () => {};
const someObj = {
  a : "ay",
  b : "bee",
  c : "si"
};

console.log(_thisIsUndefined); // undefined
console.log(doNothing()); // undefined
console.log(someObj["d"]); // undefined
```

`null` 是『不代表任何值的值』。`null`是已明确定义给变量的值。在此示例中，当`fs.readFile`方法未引发错误时，我们将获得`null`值。

```
fs.readFile('path/to/file', (e,data) => {
   console.log(e); // 当没有错误发生时，打印 null
   if(e){
     console.log(e);
   }
   console.log(data);
 });
```

在比较`null`和`undefined`时，我们使用`==`时得到`true`，使用`===`时得到`false`:

```
console.log(null == undefined); // true
console.log(null === undefined); // false
```


### [9、事件委托？有什么好处?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#9事件委托有什么好处)  


利用冒泡的原理，把事件加到父级上，触发执行效果

好处：新添加的元素还会有之前的事件；提高性能。


### [10、什么是AJAX？如何实现？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题及答案附答案汇总.md#10什么是ajax如何实现)  


`ajax`是一种能够实现局部网页刷新的技术，可以使网页异步刷新。

`ajax`的实现主要包括四个步骤：

**1、** 创建核心对象`XMLhttpRequest`；

**2、** 利用`open`方法打开与服务器的连接；

**3、** 利用`send`方法发送请求；（"POST"请求时，还需额外设置请求头）

**4、** 监听服务器响应，接收返回值。

```
//1-创建核心对象
//该对象有兼容问题，低版本浏览器应使用ActiveXObject
const xthhp = new XMLHttpRequest();
//2-连接服务器
//open(method,url,async)
xhttp.open("POST", "http://localhost:3000", true)
//设置请求头
xmlHttp.setRequestHeader("Content-Type", "application/x-www-form-urlencoded")；
//3-发送请求
//send方法发送请求参数，如为GET方法，则在open中url后拼接
xhttp.send({
    _id: 123
})
//4-接收服务器响应
//onreadystatechange事件，会在xhttp的状态发生变化时自动调用
xhttp.onreadystatechange = function() {
    //状态码共5种：0-未open  1-已open  2-已send  3-读取响应  4-响应读取结束
    if (xhttp.readyState == 4 && xhttp.status == 200) {
        alert("ajax请求已完成")
    }
}
```


### 11、什么是执行上下文和执行栈？
### 12、如何检查对象中是否存在某个属性？
### 13、$$.map和$$.each有什么区别###
### 14、简述下工作流程###
### 15、defer和async
### 16、'use strict' 是干嘛用的？
### 17、split() join()?
### 18、介绍js有哪些内置对象？
### 19、什么是构造函数？与普通函数有什么区别?
### 20、什么是移动端的300ms延迟？什么是点击穿透？解决方案?
### 21、上一个项目是什么？主要负责哪些？购物车流程?支付功能?
### 22、如何在不使用`%`模运算符的情况下检查一个数字是否是偶数？
### 23、Jq中 attr 和 prop 有什么区别###
### 24、那些操作会造成内存泄漏？
### 25、如何理解同步和异步？
### 26、JS是如何实现异步的？
### 27、call和apply 有什么好处？
### 28、AJAX 是什么？
### 29、什么是箭头函数？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




