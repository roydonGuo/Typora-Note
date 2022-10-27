# JavaScript最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、什么是作用域？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#1什么是作用域)  


JavaScript 中的作用域是我们可以有效访问变量或函数的区域。JS 有三种类型的作用域：**全局作用域**、**函数作用域**和**块作用域(ES6)**。

**全局作用域**——在全局命名空间中声明的变量或函数位于全局作用域中，因此在代码中的任何地方都可以访问它们。

```
//global namespace
var g = "global";

function globalFunc(){
  function innerFunc(){
    console.log(g); // can access "g" because "g" is a global variable
  }
 innerFunc();
}
```

**函数作用域**——在函数中声明的变量、函数和参数可以在函数内部访问，但不能在函数外部访问。

```
function myFavoriteFunc(a) {
  if (true) {
    var b = "Hello " + a;
  }
  return b;
}

myFavoriteFunc("World");

console.log(a); // Throws a ReferenceError "a" is not defined
console.log(b); // does not continue here
```

- **块作用域**-在块`{}`中声明的变量（`let，const`）只能在其中访问。

```
function testBlock(){
   if(true){
     let z = 5;
   }
   return z; 
 }

 testBlock(); // Throws a ReferenceError "z" is not defined
```

作用域也是一组用于查找变量的规则。如果变量在当前作用域中不存在，它将向外部作用域中查找并搜索，如果该变量不存在，它将再次查找直到到达全局作用域，如果找到，则可以使用它，否则引发错误，这种查找过程也称为**作用域链**。

```
/* 作用域链

 内部作用域->外部作用域-> 全局作用域
*/

// 全局作用域
var variable1 = "Comrades";   
var variable2 = "Sayonara";

function outer(){
// 外部作用域
var variable1 = "World";
function inner(){
// 内部作用域
  var variable2 = "Hello";
  console.log(variable2 + " " + variable1);
}
inner();
}  
outer(); // Hello World
```


### [2、ajax 和 jsonp ？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#2ajax-和-jsonp-)  


**ajax和jsonp的区别：**

相同点：都是请求一个url

不同点：ajax的核心是通过xmlHttpRequest获取内容

jsonp的核心则是动态添加



### [3、js延迟加载的方式有哪些？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#3js延迟加载的方式有哪些)  


`defer`和`async`、动态创建`DOM`方式（用得最多）、按需异步载入`js`


### [4、Object.seal 和 Object.freeze 方法之间有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#4objectseal-和-objectfreeze-方法之间有什么区别)  


**Object.freeze()**

`Object.freeze()` 方法可以冻结一个对象。一个被冻结的对象再也不能被修改；冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。此外，冻结一个对象后该对象的原型也不能被修改`。freeze()` 返回和传入的参数相同的对象。

**Object.seal()**

```
Object.seal()方法封闭一个对象，阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要可写就可以改变。
```

方法的相同点：

**1、** ES5新增。

**2、** 对象不可能扩展，也就是不能再添加新的属性或者方法。

**3、** 对象已有属性不允许被删除。

**4、** 对象属性特性不可以重新配置。

方法不同点：

- `Object.seal`方法生成的密封对象，如果属性是可写的，那么可以修改属性值。`* Object.freeze`方法生成的冻结对象，属性都是不可写的，也就是属性值无法更改。


### [5、Jq中如何实现多库并存?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#5jq中如何实现多库并存)  


Noconfict 多库共存就是“$ ”符号的冲突。

**方法一**：

利用jQuery的实用函数$$.noConflict();这个函数归还$$的名称控制权给另一个库，因此可以在页面上使用其他库。这时，我们可以用"jQuery "这个名称调用jQuery的功能。 $.noConflict();

```
jQuery('\#id').hide();
.....
//或者给jQuery一个别名
var $j=jQuery
$j('\#id').hide();
```

**方法二**： `(function($)\{\})(jQuery)`

**方法三**： `jQuery(function($)\{\})`

通过传递一个函数作为jQuery的参数，因此把这个函数声明为就绪函数。 我们声明$为就绪函数的参数，因为jQuery总是吧jQuery对象的引用作为第一个参数传递，所以就保证了函数的执行。


### [6、怎么理解Promise对象？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#6怎么理解promise对象)  


**`Promise`对象有如下两个特点：**

**1、** 对象的状态不受外界影响。`Promise`对象共有三种状态`pending`、`fulfilled`、`rejected`。状态值只会被异步结果决定，其他任何操作无法改变。

**2、** 状态一旦成型，就不会再变，且任何时候都可得到这个结果。状态值会由`pending`变为`fulfilled`或`rejected`，这时即为`resolved`。

**Promise的缺点有如下三个缺点：**

**1、** `Promise`一旦执行便无法被取消；

**2、** 不可设置回调函数，其内部发生的错误无法捕获；

**3、** 当处于`pending`状态时，无法得知其具体发展到了哪个阶段。

**`Pomise`中常用的方法有：**

**1、** `Promise.prototype.then()`：`Promise`实例的状态发生改变时，会调用`then`内部的回调函数。`then`方法接受两个参数（第一个为`resolved`状态时时执行的回调，第一个为`rejected`状态时时执行的回调）

**2、** `Promise.prototype.catch()`：`.then(null, rejection)`或`.then(undefined, rejection)`的别名，用于指定发生错误时的回调函数。


### [7、`in` 运算符和 `Object.hasOwnProperty` 方法有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#7in-运算符和-objecthasownproperty-方法有什么区别)  


**hasOwnPropert方法**

`hasOwnPropert()`方法返回值是一个布尔值，指示对象自身属性中是否具有指定的属性，因此这个方法会忽略掉那些从原型链上继承到的属性。

看下面的例子：

```
Object.prototype.phone= '15345025546';

let obj = {
  name: 'kyle',
  age: '28'
}
console.log(obj.hasOwnProperty('phone')) // false
console.log(obj.hasOwnProperty('name')) // true
```

可以看到，如果在函数原型上定义一个变量`phone`，`hasOwnProperty`方法会直接忽略掉。

**in 运算符**

如果指定的属性在指定的对象或其原型链中，则`in` 运算符返回`true`。

还是用上面的例子来演示：

`console.log('phone' in obj) // true`

可以看到`in`运算符会检查它或者其原型链是否包含具有指定名称的属性。


### [8、同步和异步的区别?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#8同步和异步的区别)  


**1、** 同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,进行下一步操作

**2、** 异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容


### [9、说说严格模式的限制](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#9说说严格模式的限制)  


**1、** 变量必须声明后再使用

**2、** 函数的参数不能有同名属性，否则报错

**3、** 不能使用`with`语句

**4、** 禁止`this`指向全局对象


### [10、常见兼容性问题？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新面试题，2021年面试题及答案汇总.md#10常见兼容性问题)  


**1、** `png24`位的图片在iE6浏览器上出现背景，解决方案是做成`PNG8`

**2、** 浏览器默认的`margin`和`padding`不同。解决方案是加一个全局的`*{margin:0;padding:0;}`来统一,，但是全局效率很低，一般是如下这样解决：

```
body,ul,li,ol,dl,dt,dd,form,input,h1,h2,h3,h4,h5,h6,p{
    margin:0;
    padding:0;
}
```

`IE`下,`event`对象有`x`,`y`属性,但是没有`pageX`,`pageY`属性

`Firefox`下,`event`对象有`pageX`,`pageY`属性,但是没有`x,y`属性.


### 11、Jq绑定事件的几种方式？on bind ?
### 12、call & apply 两者之间的区别###
### 13、同步和异步的区别?
### 14、什么是 event.currentTarget？？
### 15、typeof？typeof [ ]返回数据类型是？
### 16、如何知道是否在元素中使用了`event.preventDefault()`方法？
### 17、Promise 是什么？
### 18、eval是做什么的？
### 19、判断数据类型的方法有哪些？
### 20、== 和 === 有什么区别？
### 21、javascript有哪些方法定义对象
### 22、如何通过原生js 判断一个元素当前是显示还是隐藏状态?
### 23、与深拷贝有何区别？如何实现？
### 24、事件流?事件捕获？事件冒泡？
### 25、ajax 是什么?
### 26、变量作用域?
### 27、promise###
### 28、什么是事件捕获？
### 29、如何解决跨域问题?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




