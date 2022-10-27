# JavaScript最新2022年面试题及答案，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Jq中有几种选择器?分别是什么?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#1jq中有几种选择器分别是什么)  


层叠选择器、基本过滤选择器、内容过滤选择器、可视化过滤选择器、属性过滤选择器、子元素过滤选择器、表单元素选择器、表单元素过滤选择器


### [2、`Function.prototype.call` 方法的用途是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#2functionprototypecall-方法的用途是什么)  


`call()` 方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数。

`const details = {

message: 'Hello World!'

};

function getMessage(){

return this.message;

}

getMessage.call(details); // 'Hello World!'

`

注意：该方法的语法和作用与 `apply()` 方法类似，只有一个区别，就是 `call()` 方法接受的是一个参数列表，而 `apply()` 方法接受的是一个包含多个参数的数组。

```
const person = {
  name: "Marko Polo"
};

function greeting(greetingMessage) {
  return `${greetingMessage} ${this.name}`;
}

greeting.call(person, 'Hello'); // "Hello Marko Polo!"
```


### [3、什么是模板字符串？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#3什么是模板字符串)  


模板字符串是在 JS 中创建字符串的一种新方法。我们可以通过使用反引号使模板字符串化。

```
//ES5 Version
var greet = 'Hi I\'m Mark';

//ES6 Version
let greet = `Hi I'm Mark`;
```

在 ES5 中我们需要使用一些转义字符来达到多行的效果，在模板字符串不需要这么麻烦：

```
//ES5 Version
var lastWords = '\n'
  + '   I  \n'
  + '   Am  \n'
  + 'Iron Man \n';

//ES6 Version
let lastWords = `
    I
    Am
  Iron Man   
`;
```

在ES5版本中，我们需要添加`\n`以在字符串中添加新行。在模板字符串中，我们不需要这样做。

```
//ES5 Version
function greet(name) {
  return 'Hello ' + name + '!';
}

//ES6 Version
function greet(name) {
  return `Hello ${name} !`;
}
```

在 ES5 版本中，如果需要在字符串中添加表达式或值，则需要使用`+`运算符。在模板字符串s中，我们可以使用`${expr}`嵌入一个表达式，这使其比 ES5 版本更整洁。


### [4、js的几种继承方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#4js的几种继承方式)  


**1、** 使用对象冒充实现继承

**2、** 采用call、Apply方法改变函数上下文实现继承

**3、** 原型链方式继承


### [5、this是什么 在不同场景中分别代表什么###](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#5this是什么-在不同场景中分别代表什么###)  


（1）function a(){ this ?} //This:指向windows

（2）function b(){ return function(){ this ?}}b()(); //This:指向windows

（3）function c(){ return {s:function(){this}}}c().s(); //This:指向object

由于其运行期绑定的特性，JavaScript 中的 this 含义要丰富得多，它可以是全局对象、当前对象或者任意对象，这完全取决于函数的调用方式。


### [6、如何使用storage 对js文件进行缓存](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#6如何使用storage-对js文件进行缓存)  


由于sessionStorage - 针对一个 session 的数据存储，所以我们一般利用localStorage储存js文件，只有在第一次访问该页面的时候加载js文件，以后在访问的时候加载本地localStorage执行


### [7、如何创建一个对象？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#7如何创建一个对象)  


**1、** 工厂模式

**2、** 构造函数模式

**3、** 原型模式

**4、** 混合构造函数和原型模式

**5、** 动态原型模式

**6、** 寄生构造函数模式

**7、** 稳妥构造函数模式

**程序的设计模式?工厂模式?发布订阅?  **

**1、** 设计模式并不是某种语言的某块代码，设计模式是一种思想，提供给在编码时候遇到的各种问题是可以采取的解决方案，更倾向于一种逻辑思维，而不是万能代码块。

设计模式主要分三个类型:创建型、结构型和行为型。

创建型模式：单例模式，抽象工厂模式，建造者模式，工厂模式与原型模式。

结构型模式：适配器模式，桥接模式，装饰者模式，组合模式，外观模式，享元模式以及代理模式。

行为型模式：模板方法模式，命令模式，迭代器模式，观察者模式，中介者模式，备忘录模式，解释器模式，状态模式，策略模式，职责链模式和访问者模式。

**2、** 与创建型模式类似，工厂模式创建对象（视为工厂里的产品）是无需指定创建对象的具体类。

工厂模式定义一个用于创建对象的接口，这个接口由子类决定实例化哪一个类。该模式使一个类的实例化延迟到了子类。而子类可以重写接口方法以便创建的时候指定自己的对象类型。

**3、** 观察者模式又叫做发布订阅模式，它定义了一种一对多的关系，让多个观察者对象同时监听某一个主题对象，这个主题对象的状态发生改变时就会通知所有观察着对象。它是由两类对象组成，主题和观察者，主题负责发布事件，同时观察者通过订阅这些事件来观察该主体，发布者和订阅者是完全解耦的，彼此不知道对方的存在，两者仅仅共享一个自定义事件的名称。

( 设计模式实在是太高深了，小伙伴门结合网上实例自行学习，我实在是无能为力啊 )


### [8、什么是回调函数？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#8什么是回调函数)  


**回调函数**是一段可执行的代码段，它作为一个参数传递给其他的代码，其作用是在需要的时候方便调用这段（回调函数）代码。

在JavaScript中函数也是对象的一种，同样对象可以作为参数传递给函数，因此函数也可以作为参数传递给另外一个函数，这个作为参数的函数就是回调函数。

```
const btnAdd = document.getElementById('btnAdd');

btnAdd.addEventListener('click', function clickCallback(e) {
    // do something useless
});
```

在本例中，我们等待`id`为`btnAdd`的元素中的`click`事件，如果它被单击，则执行`clickCallback`函数。回调函数向某些数据或事件添加一些功能。

数组中的`reduce`、`filter`和`map`方法需要一个回调作为参数。回调的一个很好的类比是，当你打电话给某人，如果他们不接，你留下一条消息，你期待他们回调。调用某人或留下消息的行为是事件或数据，回调是你希望稍后发生的操作。


### [9、commonjs?requirejs?AMD|CMD|UMD?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#9commonjsrequirejs||)  


**1、** CommonJS就是为JS的表现来制定规范，NodeJS是这种规范的实现，webpack 也是以CommonJS的形式来书写。因为js没有模块的功能，所以CommonJS应运而生。但它不能在浏览器中运行。 CommonJS定义的模块分为:{模块引用(require)} {模块定义(exports)} {模块标识(module)}

**2、** RequireJS 是一个JavaScript模块加载器。 RequireJS有两个主要方法(method): define()和require()。这两个方法基本上拥有相同的定义(declaration) 并且它们都知道如何加载的依赖关系，然后执行一个回调函数(callback function)。与require()不同的是， define()用来存储代码作为一个已命名的模块。 因此define()的回调函数需要有一个返回值作为这个模块定义。这些类似被定义的模块叫作AMD (Asynchronous Module Definition，异步模块定义)。

**3、** AMD 是 RequireJS 在推广过程中对模块定义的规范化产出 AMD异步加载模块。它的模块支持对象 函数 构造器 字符串 JSON等各种类型的模块。 适用AMD规范适用define方法定义模块。

**4、** CMD是SeaJS 在推广过程中对模块定义的规范化产出

AMD与CDM的区别：

（1）对于于依赖的模块，AMD 是提前执行(好像现在也可以延迟执行了)，CMD 是延迟执行。

（2）AMD 推崇依赖前置，CMD 推崇依赖就近。

（3）AMD 推崇复用接口，CMD 推崇单用接口。

（4）书写规范的差异。

**5、** umd是AMD和CommonJS的糅合。

AMD 浏览器第一的原则发展 异步加载模块。

CommonJS模块以服务器第一原则发展，选择同步加载，它的模块无需包装(unwrapped modules)。这迫使人们又想出另一个更通用的模式UMD ( Universal Module Definition ), 希望解决跨平台的解决方案。UMD先判断是否支持Node.js的模块( exports )是否存在，存在则使用Node.js模块模式。


### [10、平时工作中怎么样进行数据交互?如果后台没有提供数据怎么样进行开发?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题及答案，汇总版.md#10平时工作中怎么样进行数据交互如果后台没有提供数据怎么样进行开发)  


**mock数据与后台返回的格式不同意怎么办?**

由后台编写接口文档、提供数据接口实、前台通过ajax访问实现数据交互；

在没有数据的情况下寻找后台提供静态数据或者自己定义mock数据；

返回数据不统一时编写映射文件 对数据进行映射。


### 11、如何在一行中计算多个表达式的值？
### 12、Javascript如何实现继承？
### 13、为什么在调用这个函数时，代码中的`b`会变成一个全局变量?
### 14、手动实现`Array.prototype.reduce`方法
### 15、如何copy一个dom元素？
### 16、如何添加一个dom对象到body中?innerHTML和innerText区别?
### 17、手动实现 `Array.prototype.map 方法`
### 18、手动实现缓存方法
### 19、null，undefined 的区别？
### 20、什么是高阶函数？
### 21、|| 运算符能做什么
### 22、通过new创建一个对象的时候，函数内部有哪些改变###
### 23、什么是NaN？以及如何检查值是否为NaN？
### 24、**
### 25、Function.prototype.apply 方法的用途是什么？
### 26、那些操作会造成内存泄漏？
### 27、为什么要有同源限制？
### 28、DOM事件模型和事件流？
### 29、编写一个 getElementsByClassName 封装函数?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




