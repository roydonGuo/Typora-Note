# JavaScript最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Node的应用场景](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#1node的应用场景)  


**特点：**

**1、** 它是一个`Javascript`运行环境

**2、** 依赖于`Chrome V8`引擎进行代码解释

**3、** 事件驱动

**4、** 非阻塞`I/O`

**5、** 单进程，单线程

**优点：**

**1、** 高并发（最重要的优点）

**缺点：**

**1、** 只支持单`核CPU`，不能充分利用`CPU`

**2、** 可靠性低，一旦代码某个环节崩溃，整个系统都崩溃


### [2、异步编程？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#2异步编程)  


**方法1：**

**1、** 回调函数，优点是简单、容易理解和部署，缺点是不利于代码的阅读和维护，各个部分之间高度耦合（Coupling），流程会很混乱，而且每个任务只能指定一个回调函数。

**方法2：**

**1、** 时间监听，可以绑定多个事件，每个事件可以指定多个回调函数，而且可以“去耦合”（Decoupling），有利于实现模块化。缺点是整个程序都要变成事件驱动型，运行流程会变得很不清晰。

**方法3：**

发布/订阅，性质与“事件监听”类似，但是明显优于后者。

**方法4：**

**1、** Promises对象，是CommonJS工作组提出的一种规范，目的是为异步编程提供统一接口。

**2、** 简单说，它的思想是，每一个异步任务返回一个Promise对象，该对象有一个then方法，允许指定回调函数。


### [3、event.preventDefault() 和 event.stopPropagation()方法之间有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#3eventpreventdefault-和-eventstoppropagation方法之间有什么区别)  


`event.preventDefault()` 方法可防止元素的默认行为。如果在表单元素中使用，它将阻止其提交。如果在锚元素中使用，它将阻止其导航。如果在上下文菜单中使用，它将阻止其显示或显示。`event.stopPropagation()`方法用于阻止捕获和冒泡阶段中当前事件的进一步传播。


### [4、作用域和执行上下文的区别是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#4作用域和执行上下文的区别是什么)  


**1、** 函数的执行上下文只在函数被调用时生成，而其作用域在创建时已经生成；

**2、** 函数的作用域会包含若干个执行上下文(有可能是零个，当函数未被调用时)。


### [5、Ajax原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#5ajax原理)  


**1、** `Ajax`的原理简单来说是在用户和服务器之间加了—个中间层(`AJAX`引擎)，通过`XmlHttpRequest`对象来向服务器发异步请求，从服务器获得数据，然后用`javascrip`t来操作`DOM`而更新页面。使用户操作与服务器响应异步化。这其中最关键的一步就是从服务器获得请求数据

**2、** `Ajax`的过程只涉及`JavaScript`、`XMLHttpRequest`和`DOM`。`XMLHttpRequest`是`aja`x的核心机制

```
 // 1、创建连接
    var xhr = null;
    xhr = new XMLHttpRequest()
    // 2、连接服务器
    xhr.open('get', url, true)
    // 3、发送请求
    xhr.send(null);
    // 4、接受请求
    xhr.onreadystatechange = function(){
        if(xhr.readyState == 4){
            if(xhr.status == 200){
                success(xhr.responseText);
            } else { // fail
                fail && fail(xhr.status);
            }
        }
    }
```


### [6、["1", "2", "3"].map(parseInt) 答案是多少？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#6["1",-"2",-"3"]mapparseint-答案是多少)  


`[1, NaN, NaN]`因为 `parseInt` 需要两个参数 `(val, radix)`，其中`radix` 表示解析时用的基数。

`map`传了 `3`个`(element, index, array)`，对应的 `radix` 不合法导致解析失败。


### [7、25.Jq如何判断元素显示隐藏？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#725jq如何判断元素显示隐藏)  


```
//第一种：使用CSS属性 
var display =$('#id').css('display'); 
if(display == 'none'){    alert("我是隐藏的！"); }
//第二种：使用jquery内置选择器 
<div id="test"<p>仅仅是测试所用</p</div>
if($("#test").is(":hidden")){        $("#test").show();    //如果元素为隐藏,则将它显现 }else{       $("#test").hide();     //如果元素为显现,则将其隐藏 }
//第三种：jQuery判断元素是否显示 是否隐藏
var node=$('#id');
if(node.is(':hidden')){　　//如果node是隐藏的则显示node元素，否则隐藏
　　node.show();　
}else{
　　node.hide();
}
```


### [8、同步异步?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#8同步异步)  


**1、** 进程同步：就是在发出一个功能调用时，在没有得到结果之前，该调用就不返回。也就是必须一件一件事做,等前一件做完了才能做下一件事

**2、** 异步的概念和同步相对。当一个异步过程调用发出后，调用者不能立刻得到结果。实际处理这个调用的部件在完成后，通过状态、通知和回调来通知调用者。


### [9、你对数据校验是怎么样处理的？jquery.validate？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#9你对数据校验是怎么样处理的jqueryvalidate)  


通俗的说，就是为保证数据的完整性，用一种指定的算法对原始数据计算出的一个校验值。接收方用同样的算法计算一次校验值，如果和随数据提供的校验值一样，就说明数据是完整的。

用正则表达式来处理;

jquery.validate：为表单验证插件


### [10、自执行函数?用于什么场景？好处?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题2021年，常见面试题及答案汇总.md#10自执行函数用于什么场景好处)  


**自执行函数:**

**1、** 声明一个匿名函数

**2、** 马上调用这个匿名函数。

作用：创建一个独立的作用域。

**好处：**

防止变量弥散到全局，以免各种js库冲突。隔离作用域避免污染，或者截断作用域链，避免闭包造成引用变量无法释放。利用立即执行特性，返回需要的业务函数或对象，避免每次通过条件判断来处理

场景：一般用于框架、插件等场景


### 11、异步加载JS的方式有哪些？
### 12、如何确保ajax或连接不走缓存路径
### 13、什么是原型、原型链？
### 14、什么是提升？
### 15、Jq中get和eq有什么区别？
### 16、为什么typeof null 返回 object？如何检查一个值是否为 null？
### 17、节点类型?判断当前节点类型?
### 18、this指向的各种情况都有什么？
### 19、有哪些方法可以处理 JS 中的异步代码？
### 20、什么是闭包？
### 21、怎么理解宏任务，微任务？？？
### 22、html和xhtml有什么区别?
### 23、EventLoop事件循环是什么？
### 24、使用 + 或一元加运算符是将字符串转换为数字的最快方法吗？
### 25、Function.prototype.apply 和 Function.prototype.call 之间有什么区别？
### 26、arguments 的对象是什么？
### 27、Function.prototype.bind 的用途是什么？
### 28、谈谈你对ES6的理解
### 29、`require`/`import`之间的区别？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




