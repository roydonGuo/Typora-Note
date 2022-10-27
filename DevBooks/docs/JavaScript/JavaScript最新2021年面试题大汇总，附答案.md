# JavaScript最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)


### [1、为什么在 JS 中比较两个相似的对象时返回 false？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#1为什么在-js-中比较两个相似的对象时返回-false)  


先看下面的例子：

```
let a = { a: 1 };
let b = { a: 1 };
let c = a;
console.log(a === b); // 打印 false，即使它们有相同的属性
console.log(a === c); // true
```

JS 以不同的方式比较对象和基本类型。在基本类型中，JS 通过值对它们进行比较，而在对象中，JS 通过引用或存储变量的内存中的地址对它们进行比较。这就是为什么第一个`console.log`语句返回`false`，而第二个`console.log`语句返回`true`。`a`和`c`有相同的引用地址，而`a`和`b`没有。


### [2、函数表达式和函数声明之间有什么区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#2函数表达式和函数声明之间有什么区别)  


看下面的例子：

```
hoistedFunc();
notHoistedFunc();

function hoistedFunc(){
  console.log("注意：我会被提升");
}

var notHoistedFunc = function(){
  console.log("注意：我没有被提升");
}
```

`notHoistedFunc`调用抛出异常：`Uncaught TypeError: notHoistedFunc is not a function`，而`hoistedFunc`调用不会，因为`hoistedFunc`会被提升到作用域的顶部，而`notHoistedFunc` 不会。


### [3、常见web安全及防护原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#3常见web安全及防护原理)  


**`sql`注入原理**

就是通过把`SQL`命令插入到`Web`表单递交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令

**总的来说有以下几点**

永远不要信任用户的输入，要对用户的输入进行校验，可以通过正则表达式，或限制长度，对单引号和双`"-"`进行转换等

**1、** 永远不要使用动态拼装SQL，可以使用参数化的`SQL`或者直接使用存储过程进行数据查询存取

**2、** 永远不要使用管理员权限的数据库连接，为每个应用使用单独的权限有限的数据库连接

**3、** 不要把机密信息明文存放，请加密或者`hash`掉密码和敏感的信息

**XSS原理及防范**

`Xss(cross-site scripting)`攻击指的是攻击者往`Web`页面里插入恶意`html`标签或者`javascript`代码。

**比如：**

攻击者在论坛中放一个看似安全的链接，骗取用户点击后，窃取`cookie`中的用户私密信息；或者攻击者在论坛中加一个恶意表单，当用户提交表单的时候，却把信息传送到攻击者的服务器中，而不是用户原本以为的信任站点

**XSS防范方法**

首先代码里对用户输入的地方和变量都需要仔细检查长度和对`”<”,”>”,”;”,”’”`等字符做过滤；其次任何内容写到页面之前都必须加以encode，避免不小心把`html tag` 弄出来。这一个层面做好，至少可以堵住超过一半的XSS 攻击

**XSS与CSRF有什么区别吗？**

**1、** `XSS`是获取信息，不需要提前知道其他用户页面的代码和数据包。`CSRF`是代替用户完成指定的动作，需要知道其他用户页面的代码和数据包。要完成一次`CSRF`攻击，受害者必须依次完成两个步骤

**2、** 登录受信任网站`A`，并在本地生成`Cookie`

**3、** 在不登出`A`的情况下，访问危险网站`B`

**CSRF的防御**

服务端的`CSRF`方式方法很多样，但总的思想都是一致的，就是在客户端页面增加伪随机数

通过验证码的方法


### [4、有哪些数据类型？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#4有哪些数据类型)  


根据 JavaScript 中的变量类型传递方式，分为基本数据类型和引用数据类型两大类七种。

基本数据类型包括Undefined、Null、Boolean、Number、String、Symbol (ES6新增)六种。 引用数据类型只有Object一种，主要包括对象、数组和函数。

**判断数据类型采用`typeof`操作符，有两种语法：**

```
typeof 123;//语法一

const FG = 123;
typeof FG;//语法二

typeof(null) //返回 object;
null == undefined //返回true，因为undefined派生自null;
null === undefined //返回false。
```


### [5、简述一下你理解的面向对象？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#5简述一下你理解的面向对象)  


面向对象是基于万物皆对象这个哲学观点、把一个对象抽象成类,具体上就是把一个对象的静态特征和动态特征抽象成属性和方法,也就是把一类事物的算法和数据结构封装在一个类之中,程序就是多个对象和互相之间的通信组成的、

面向对象具有封装性,继承性,多态性。

封装:隐蔽了对象内部不需要暴露的细节,使得内部细节的变动跟外界脱离,只依靠接口进行通信.封装性降低了编程的复杂性、通过继承,使得新建一个类变得容易,一个类从派生类那里获得其非私有的方法和公用属性的繁琐工作交给了编译器、而 继承和实现接口和运行时的类型绑定机制 所产生的多态,使得不同的类所产生的对象能够对相同的消息作出不同的反应,极大地提高了代码的通用性、

总之,面向对象的特性提高了大型程序的重用性和可维护性.


### [6、如何清除一个定时器?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#6如何清除一个定时器)  


window.clearInterval();

window.clearTimeout();


### [7、Gc机制是什么？为什么闭包不会被回收变量和函数？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#7gc机制是什么为什么闭包不会被回收变量和函数)  


**1、** Gc垃圾回收机制;

**2、** 外部变量没释放，所以指向的大函数内的小函数也释放不了


### [8、为什么此代码 `obj.someprop.x` 会引发错误?](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#8为什么此代码-objsomepropx-会引发错误)  


```
const obj = {};console.log(obj.someprop.x);
```

显然，由于我们尝试访问`someprop`属性中的`x`属性，而 someprop 并没有在对象中，所以值为 `undefined`。记住对象本身不存在的属性，并且其原型的默认值为`undefined`。因为`undefined`没有属性`x`，所以试图访问将会报错。


### [9、说几条写JavaScript的基本规范？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#9说几条写javascript的基本规范)  


**1、** 不要在同一行声明多个变量

**2、** 请使用`===/!==`来比较`true/false`或者数值

**3、** 使用对象字面量替代`new Array`这种形式

**4、** 不要使用全局函数

**5、** `Switch`语句必须带有`default`分支

**6、** `If`语句必须使用大括号

**7、** `for-in`循环中的变量 应该使用`var`关键字明确限定作用域，从而避免作用域污


### [10、JavaScript原型，原型链 ? 有什么特点？](https://gitee.com/souyunku/DevBooks/blob/master/docs/JavaScript/JavaScript最新2021年面试题大汇总，附答案.md#10javascript原型原型链--有什么特点)  


在JavaScript中,一共有两种类型的值,原始值和对象值.每个对象都有一个内部属性[[prototype]],我们通常称之为原型.原型的值可以是一个对象,也可以是null.如果它的值是一个对象,则这个对象也一定有自己的原型.这样就形成了一条线性的链,我们称之为原型链、

访问一个对象的原型可以使用ES5中的Object.getPrototypeOf方法,或者ES6中的__proto__属性、原型链的作用是用来实现继承,比如我们新建一个数组,数组的方法就是从数组的原型上继承而来的。


### 11、offsetWidth/offsetHeight,clientWidth/clientHeight与scrollWidth/scrollHeight的区别
### 12、jsonp原理？ 缺点?
### 13、disabled readyonly?
### 14、javascript 代码中的"use strict";是什么意思 ? 使用它区别是什么？
### 15、XML和JSON的区别？
### 16、数据持久化技术(ajax)?简述ajax流程###
### 17、JSON 的了解？
### 18、ajax的缺点
### 19、什么是作用域和作用域链？
### 20、&& 运算符能做什么
### 21、几种基本数据类型?复杂数据类型?值类型和引用数据类型?堆栈数据结构
### 22、什么是事件传播?
### 23、window.onload ==? DOMContentLoaded ?
### 24、什么是包装对象（wrapper object）？
### 25、DOM 是什么？
### 26、谈谈你对webpack的看法
### 27、JSON 的了解？**
### 28、何为防抖和节流？如何实现？
### 29、在jq中 mouseover mouseenter mouseout mouseleave 和 hover有什么关联?




## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




