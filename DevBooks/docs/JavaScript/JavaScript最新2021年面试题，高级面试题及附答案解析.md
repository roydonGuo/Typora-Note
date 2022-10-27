# JavaScript最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、强制转换 显式转换 隐式转换?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#1强制转换-显式转换-隐式转换)  


```
//强制类型转换：
Boolean(0)   // =false - 零
Boolean(new object())   // =true - 对象
Number(undefined)       // =  NaN
Number(null)              // =0
String(null)              // ="null"
parseInt( )
parseFloat( )
JSON.parse( )
JSON.stringify ( )
```

隐式类型转换：

在使用算术运算符时，运算符两边的数据类型可以是任意的，比如，一个字符串可以和数字相加。之所以不同的数据类型之间可以做运算，是因为JavaScript引擎在运算之前会悄悄的把他们进行了隐式类型转换的

```
（例如：x+"" //等价于String(x)  
\+x //等价于Number(x)  
x-0 //同上  
!!x //等价于Boolean(x),是双叹号）
```

**显式转换：**

如果程序要求一定要将某一类型的数据转换为另一种类型，则可以利用强制类型转换运算符进行转换，这种强制转换过程称为显示转换。

显示转换是你定义让这个值类型转换成你要用的值类型，是底到高的转换。例 int 到float就可以直接转，int i=5,想把他转换成char类型，就用显式转换（char）i


### [2、JavaScript 中的虚值是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#2javascript-中的虚值是什么)  


`const falsyValues = ['', 0, null, undefined, NaN, false];`

简单的来说虚值就是是在转换为布尔值时变为 `false` 的值。


### [3、简述ajax执行流程](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#3简述ajax执行流程)  


```
基本步骤：
var xhr =null;//创建对象 
if(window.XMLHttpRequest){
       xhr = new XMLHttpRequest();
}else{
       xhr = new ActiveXObject("Microsoft.XMLHTTP");
}
xhr.open(“方式”,”地址”,”标志位”);//初始化请求 
   xhr.setRequestHeader(“”,””);//设置http头信息 
xhr.onreadystatechange =function(){}//指定回调函数 
xhr.send();//发送请求
```


### [4、null，undefined 的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#4nullundefined-的区别)  


undefined表示变量声明但未初始化的值，null表示准备用来保存对象，还没有真正保存对象的值。从逻辑角度看，null表示一个空对象指针。


### [5、attribute和property的区别是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#5attribute和property的区别是什么)  


**1、** `attribute`是`dom`元素在文档中作为`html`标签拥有的属性；

**2、** `property`就是`dom`元素在`js`中作为对象拥有的属性。

**3、** 对于`html`的标准属性来说，`attribute`和`property`是同步的，是会自动更新的

**4、** 但是对于自定义的属性来说，他们是不同步的


### [6、什么是`Set`对象，它是如何工作的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#6什么是set对象它是如何工作的)  


**Set** 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。

我们可以使用`Set`构造函数创建`Set`实例。

`const set1 = new Set(); const set2 = new Set(["a","b","c","d","d","e"]);`

我们可以使用`add`方法向`Set`实例中添加一个新值，因为`add`方法返回`Set`对象，所以我们可以以链式的方式再次使用`add`。如果一个值已经存在于`Set`对象中，那么它将不再被添加。

`set2.add("f"); set2.add("g").add("h").add("i").add("j").add("k").add("k"); // 后一个『k』不会被添加到set对象中，因为它已经存在了`

我们可以使用`has`方法检查`Set`实例中是否存在特定的值。

`set2.has("a") // true set2.has("z") // true`

我们可以使用`size`属性获得`Set`实例的长度。

`set2.size // returns 10`

可以使用`clear`方法删除 `Set` 中的数据。

`set2.clear();`

我们可以使用`Set`对象来删除数组中重复的元素。

`const numbers = [1, 2, 3, 4, 5, 6, 6, 7, 8, 8, 5]; const uniqueNums = [...new Set(numbers)]; // [1,2,3,4,5,6,7,8]`


### [7、JavaScript 中 `this` 值是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#7javascript-中-this-值是什么)  


基本上，`this`指的是当前正在执行或调用该函数的对象的值。`this`值的变化取决于我们使用它的上下文和我们在哪里使用它。

```
const carDetails = {
  name: "Ford Mustang",
  yearBought: 2005,
  getName(){
    return this.name;
  },
  isRegistered: true
};

console.log(carDetails.getName()); // Ford Mustang
```

这通常是我们期望结果的，因为在`getName`方法中我们返回`this.name`，在此上下文中，`this`指向的是`carDetails`对象，该对象当前是执行函数的“所有者”对象。

接下我们做些奇怪的事情：

```
var name = "Ford Ranger";
var getCarName = carDetails.getName;

console.log(getCarName()); // Ford Ranger
```

上面打印`Ford Ranger`，这很奇怪，因为在第一个`console.log`语句中打印的是`Ford Mustang`。这样做的原因是`getCarName`方法有一个不同的“所有者”对象，即`window`对象。在全局作用域中使用`var`关键字声明变量会在`window`对象中附加与变量名称相同的属性。请记住，当没有使用`“use strict”`时，在全局作用域中`this`指的是`window`对象。

`console.log(getCarName === window.getCarName); // true console.log(getCarName === this.getCarName); // true`

本例中的`this`和`window`引用同一个对象。

解决这个问题的一种方法是在函数中使用`apply`和`call`方法。

`console.log(getCarName.apply(carDetails)); // Ford Mustang console.log(getCarName.call(carDetails)); // Ford Mustang`

`apply`和`call`方法期望第一个参数是一个对象，该对象是函数内部`this`的值。

`IIFE`或**立即执行的函数表达式**，在全局作用域内声明的函数，对象内部方法中的匿名函数和内部函数的`this`具有默认值，该值指向`window`对象。

```
(function (){
 console.log(this);
})(); // 打印 "window" 对象

function iHateThis(){
  console.log(this);
}

iHateThis(); // 打印 "window" 对象

const myFavoriteObj = {
 guessThis(){
    function getName(){
      console.log(this.name);
    }
    getName();
 },
 name: 'Marko Polo',
 thisIsAnnoying(callback){
   callback();
 }
};

myFavoriteObj.guessThis(); // 打印 "window" 对象
myFavoriteObj.thisIsAnnoying(function (){
 console.log(this); // 打印 "window" 对象
});
```

如果我们要获取`myFavoriteObj`对象中的`name`属性（即**Marko Polo**）的值，则有两种方法可以解决此问题。

一种是将 `this` 值保存在变量中。

```
const myFavoriteObj = {
 guessThis(){
  const self = this; // 把 this 值保存在 self 变量中
  function getName(){
    console.log(self.name);
  }
  getName();
 },
 name: 'Marko Polo',
 thisIsAnnoying(callback){
   callback();
  }
};
```

第二种方式是使用箭头函数

```
const myFavoriteObj = {
  guessThis(){
     const getName = () => { 
       console.log(this.name);
     }
     getName();
  },
  name: 'Marko Polo',
  thisIsAnnoying(callback){
   callback();
  }
};
```

箭头函数没有自己的 `this`。它复制了这个封闭的词法作用域中`this`值，在这个例子中，`this`值在`getName`内部函数之外，也就是`myFavoriteObj`对象。


### [8、$$('div+.ab')和$$('.ab+div') 哪个效率高？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#8$$'div+ab'和$$'ab+div'-哪个效率高)  


$('div+.ab')效率高


### [9、什么是类？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#9什么是类)  


`类(class)`是在 JS 中编写构造函数的新方法。它是使用构造函数的语法糖，在底层中使用仍然是原型和基于原型的继承。

```
//ES5 Version
 function Person(firstName, lastName, age, address){
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
    this.address = address;
 }

 Person.self = function(){
   return this;
 }

 Person.prototype.toString = function(){
   return "[object Person]";
 }

 Person.prototype.getFullName = function (){
   return this.firstName + " " + this.lastName;
 }  

 //ES6 Version
 class Person {
    constructor(firstName, lastName, age, address){
        this.lastName = lastName;
        this.firstName = firstName;
        this.age = age;
        this.address = address;
    }

    static self() {
       return this;
    }

    toString(){
       return "[object Person]";
    }

    getFullName(){
       return `${this.firstName} ${this.lastName}`;
    }
 }
```

重写方法并从另一个类继承。

```
//ES5 Version
Employee.prototype = Object.create(Person.prototype);

function Employee(firstName, lastName, age, address, jobTitle, yearStarted) {
  Person.call(this, firstName, lastName, age, address);
  this.jobTitle = jobTitle;
  this.yearStarted = yearStarted;
}

Employee.prototype.describe = function () {
  return `I am ${this.getFullName()} and I have a position of ${this.jobTitle} and I started at ${this.yearStarted}`;
}

Employee.prototype.toString = function () {
  return "[object Employee]";
}

//ES6 Version
class Employee extends Person { //Inherits from "Person" class
  constructor(firstName, lastName, age, address, jobTitle, yearStarted) {
    super(firstName, lastName, age, address);
    this.jobTitle = jobTitle;
    this.yearStarted = yearStarted;
  }

  describe() {
    return `I am ${this.getFullName()} and I have a position of ${this.jobTitle} and I started at ${this.yearStarted}`;
  }

  toString() { // Overriding the "toString" method of "Person"
    return "[object Employee]";
  }
}
```

**所以我们要怎么知道它在内部使用原型？**

```
class Something {

}

function AnotherSomething(){

}
const as = new AnotherSomething();
const s = new Something();

console.log(typeof Something); // "function"
console.log(typeof AnotherSomething); // "function"
console.log(as.toString()); // "[object Object]"
console.log(as.toString()); // "[object Object]"
console.log(as.toString === Object.prototype.toString); // true
console.log(s.toString === Object.prototype.toString); // true
```


### [10、如何判断值是否为数组？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题，高级面试题及附答案解析.md#10如何判断值是否为数组)  


我们可以使用`Array.isArray`方法来检查值是否为**数组**。当传递给它的参数是数组时，它返回`true`，否则返回`false`。

```
console.log(Array.isArray(5));  // false
console.log(Array.isArray("")); // false
console.log(Array.isArray()); // false
console.log(Array.isArray(null)); // false
console.log(Array.isArray({ length: 5 })); // false

console.log(Array.isArray([])); // true
```

如果环境不支持此方法，则可以使用`polyfill`实现。

`function isArray(value){ return Object.prototype.toString.call(value) === "[object Array]" }`

当然还可以使用传统的方法：

`let a = [] if (a instanceof Array) { console.log('是数组') } else { console.log('非数组') }`


### 11、调用函数，可以使用哪些方法？
### 12、JavaScript原型，原型链 ? 有什么特点？
### 13、谈谈你对AMD、CMD的理解
### 14、开发时如何对项目进行管理?gulp?
### 15、一般使用什么版本控制工具?svn如何对文件加锁###
### 16、ajax中 get 和 post 有什么区别?
### 17、判断数据类型
### 18、readystate 0~4
### 19、一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？（流程说的越详细越好）
### 20、回调函数?
### 21、说说你对作用域链的理解
### 22、如何对登录的账号密码进行加密?
### 23、ECMAScript 是什么？
### 24、什么是 IIFE，它的用途是什么？
### 25、什么是函数式编程? JavaScript 的哪些特性使其成为函数式语言的候选语言？
### 26、jQuery与jQuery UI 有啥区别？
### 27、30.Jq中怎么样编写插件?
### 28、隐式和显式转换有什么区别）？
### 29、什么是缓存及它有什么作用？
### 30、如何解决跨域问题?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




