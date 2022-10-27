# JavaScript

## 基础认识

<img src="C:\Users\31330\Pictures\Typora\image-20220630233138792.png" alt="image-20220630233138792" style="zoom:67%;" />

弹出提示对话框：alert("弹出对话框")

解释型语言，一行一行解释。

```html
<script>
    alert("弹出对话框")
</script>
```

![image-20220630232744108](C:\Users\31330\Pictures\Typora\image-20220630232744108.png)

认识js

发明人：<img src="C:\Users\31330\Pictures\Typora\image-20220630233346373.png" alt="image-20220630233346373" style="zoom:50%;" />

<img src="C:\Users\31330\Pictures\Typora\image-20220630233406014.png" alt="image-20220630233406014" style="zoom:67%;" />

<img src="C:\Users\31330\Pictures\Typora\image-20220630233420755.png" alt="image-20220630233420755" style="zoom:80%;" />

运行在客户端

js的作用：

<img src="C:\Users\31330\Pictures\Typora\image-20220630233809366.png" alt="image-20220630233809366" style="zoom: 67%;" />

js的组成：

<img src="C:\Users\31330\Pictures\Typora\image-20220630234201961.png" alt="image-20220630234201961" style="zoom:80%;" />

注释：

![image-20220630234932831](C:\Users\31330\Pictures\Typora\image-20220630234932831.png)

<img src="C:\Users\31330\Pictures\Typora\image-20220630234958715.png" alt="image-20220630234958715" style="zoom:50%;" />

js的输入输出：

<img src="C:\Users\31330\Pictures\Typora\image-20220630235052332.png" alt="image-20220630235052332" style="zoom:80%;" />

prompt取值是字符型的

***

### 变量

```html
var age;//声明一个名称为age的变量，赋值var age=18;
```

只声明不赋值值为undefined

<img src="C:\Users\31330\Pictures\Typora\image-20220630235544674.png" alt="image-20220630235544674" style="zoom:80%;" />

***

## 数据类型

数据类型可变

简单（基本）数据类型

<img src="C:\Users\31330\Pictures\Typora\image-20220701001333013.png" alt="image-20220701001333013" style="zoom:80%;" />

<img src="C:\Users\31330\Pictures\Typora\image-20220701002038458.png" alt="image-20220701002038458" style="zoom:80%;" />

获取字符串String长度

```html
str.length
```

转义符

<img src="C:\Users\31330\Pictures\Typora\image-20220701002340703.png" alt="image-20220701002340703" style="zoom:80%;" />

undefined和null

<img src="C:\Users\31330\Pictures\Typora\image-20220701151212831.png" alt="image-20220701151212831" style="zoom:80%;" />

判断变量类型``typeof 变量名``

```html
<script>
    var str = 'roydon';
    alert(typeof str)//string
</script>
```

<img src="C:\Users\31330\Pictures\Typora\image-20220701151631900.png" alt="image-20220701151631900" style="zoom: 67%;" />

数据类型转换

1.转换成string

![image-20220701152018444](C:\Users\31330\Pictures\Typora\image-20220701152018444.png)

2.转换成数字型number

![image-20220701152206427](C:\Users\31330\Pictures\Typora\image-20220701152206427.png)

隐式转换

![image-20220701152420325](C:\Users\31330\Pictures\Typora\image-20220701152420325.png)

<img src="C:\Users\31330\Pictures\Typora\image-20220701152807067.png" alt="image-20220701152807067" style="zoom: 80%;" />

3.转换成布尔型boolean

![image-20220701153225169](C:\Users\31330\Pictures\Typora\image-20220701153225169.png)

![image-20220701153209075](C:\Users\31330\Pictures\Typora\image-20220701153209075.png)

![image-20220701163557995](C:\Users\31330\Pictures\Typora\image-20220701163557995.png)

***

## 数组

```html
var arr = new Array(2，3，4);//==>[2,3,4]，若参数为一个，表示数组长度，元素为空
```

或者，利用字面量创建数组

```html
var arr = ['小明','小红','小强'];
```

![image-20220703164722472](C:\Users\31330\Pictures\Typora\image-20220703164722472.png)

数组遍历：length拿数组长度

<img src="C:\Users\31330\Pictures\Typora\image-20220701170254528.png" alt="image-20220701170254528" style="zoom:80%;" />

数组排序：

![image-20220703165723657](C:\Users\31330\Pictures\Typora\image-20220703165723657.png)

<img src="C:\Users\31330\Pictures\Typora\image-20220703170011658.png" alt="image-20220703170011658" style="zoom:80%;" />

检测是否为数组：``instanceof``和``Array.isArray()``

![image-20220703165057555](C:\Users\31330\Pictures\Typora\image-20220703165057555.png)

数组操作：添加或删除

![image-20220703165508073](C:\Users\31330\Pictures\Typora\image-20220703165508073.png)

1.添加

![image-20220703165325677](C:\Users\31330\Pictures\Typora\image-20220703165325677.png)

2.删除

![image-20220703165535513](C:\Users\31330\Pictures\Typora\image-20220703165535513.png)

数组索引方法：

![image-20220703184852640](C:\Users\31330\Pictures\Typora\image-20220703184852640.png)

数组转字符串![image-20220703185657684](C:\Users\31330\Pictures\Typora\image-20220703185657684.png)

![image-20220703185724698](C:\Users\31330\Pictures\Typora\image-20220703185724698.png)

***

## 函数

声明和调用：``function``

<img src="C:\Users\31330\Pictures\Typora\image-20220701172646956.png" alt="image-20220701172646956" style="zoom:80%;" />

两种声明方式：

<img src="C:\Users\31330\Pictures\Typora\image-20220703121944484.png" alt="image-20220703121944484" style="zoom:80%;" />

return：

<img src="C:\Users\31330\Pictures\Typora\image-20220701173359006.png" alt="image-20220701173359006" style="zoom:80%;" />

arguments

内置对象，存储传递来的所有实参，保存的形式是数组（伪数组）

![image-20220703121558433](C:\Users\31330\Pictures\Typora\image-20220703121558433.png)



作用域：

全局和局部

就近

***

## 对象

对象的创建3法

```html
	<script>
        //创建对象的3种方法
        //var person={} //创建了一个空对象
        //方法1=============
        var person = {
            pname: 'roydon',
            age: 18,
            gender: 'man',
            getAge: function () {//方法
                console.log(this.age);
            }
        }
        //获取属性值的两种方法
        //1.
        console.log(person.pname);
        //2.
        console.log(person['age']);
        person.getAge();//既然是方法，就要带()
        //方法2=============
        var person1 = new Object();
        person1.pname = 'yicheng';
        person1.age = 19;
        person1.gender = 'man';
        person1.getAge = function () {
            console.log(this.age);
        }
        //获取属性两种方法同上
        console.log(person1);
        person1.getAge();
        //方法3==============构造函数法,首字母大写
        function Person3(pname, age) {
            this.pname = pname;
            this.age = age;
            this.getAge = function () {
                console.log(this.age);
            }
        }
        var person3 = new Person3('jack',20);
        person3.getAge();
    </script>
```



遍历forin：

```html
//遍历
for (const key in person3) {
	if (Object.hasOwnProperty.call(person3, key)) {
		const name = key;//属性名
        console.log(name);
        const element = person3[key];//值
        console.log(element);
     }
}
```

<img src="C:\Users\31330\Pictures\Typora\image-20220703161130532.png" alt="image-20220703161130532" style="zoom:80%;" />

<img src="C:\Users\31330\Pictures\Typora\image-20220703161922886.png" alt="image-20220703161922886" style="zoom:80%;" />

日期Date对象：

<img src="C:\Users\31330\Pictures\Typora\image-20220703163421893.png" alt="image-20220703163421893" style="zoom:67%;" />

<img src="C:\Users\31330\Pictures\Typora\image-20220703163127890.png" alt="image-20220703163127890"  />

<img src="C:\Users\31330\Pictures\Typora\image-20220703163326380.png" alt="image-20220703163326380" style="zoom: 80%;" />

获取时间戳：

<img src="C:\Users\31330\Pictures\Typora\image-20220703163636856.png" alt="image-20220703163636856"  />

时间戳转换成时分秒：

<img src="C:\Users\31330\Pictures\Typora\image-20220703163843457.png" alt="image-20220703163843457" style="zoom:80%;" />

倒计时案例：

![image-20220703164356185](C:\Users\31330\Pictures\Typora\image-20220703164356185.png)

***

## 字符串

字符串基本操作

![image-20220703191039374](C:\Users\31330\Pictures\Typora\image-20220703191039374.png)

![image-20220703191005496](C:\Users\31330\Pictures\Typora\image-20220703191005496.png)

![image-20220703191233210](C:\Users\31330\Pictures\Typora\image-20220703191233210.png)

<img src="C:\Users\31330\Pictures\Typora\image-20220703191258583.png" alt="image-20220703191258583" style="zoom:67%;" />

对象转json字符串：

JSON.stringify(obj)；

![image-20220804164954177](C:\Users\31330\Pictures\Typora\image-20220804164954177.png)

json字符串转对象：

JSON.parse(str);

![image-20220804165155499](C:\Users\31330\Pictures\Typora\image-20220804165155499.png)

***

## Web API

应用程序编程接口

![image-20220703192756675](C:\Users\31330\Pictures\Typora\image-20220703192756675.png)

***

### DOM

![image-20220703193211469](C:\Users\31330\Pictures\Typora\image-20220703193211469.png)

dom树：

![image-20220703193523977](C:\Users\31330\Pictures\Typora\image-20220703193523977.png)

每一个元素可以看作一个对象

***

#### 获取页面元素



<img src="C:\Users\31330\Pictures\Typora\image-20220704110148101.png" alt="image-20220704110148101" style="zoom:67%;" />

1. 根据ID获取（返回的是一个匹配到ID的DOM Element对象）

```html
document.getElementById();
```

可以使用``console.dir();``查看

2. 通过标签名获取（返回的是一个指定标签的集合）

```html
element.getElementByTagName();
```

3. 通过类名获取

<img src="C:\Users\31330\Pictures\Typora\image-20220704111815449.png" alt="image-20220704111815449" style="zoom:;" />

<img src="C:\Users\31330\Pictures\Typora\image-20220704112208151.png" alt="image-20220704112208151" style="zoom:80%;" />

***

#### 事件基础

例如，点击一个按钮，弹出对话框

```html
<button id="btn">
    点我
</button>
```

事件分为三部分：事件源、事件类型、事件处理程序。也叫事件三要素

```javascript
//1.事件源=事件被触发的对象（按钮）
var btn = document.getElementById('btn');
//2.事件类型=如何触发，例如：点击，鼠标悬停，按键按下
//3.事件处理程序=函数赋值
btn.onclick=function(){
	alert('点了我');
}
```

***

#### 操作元素

1. 改变元素内容

![image-20220704113516135](C:\Users\31330\Pictures\Typora\image-20220704113516135.png)

![image-20220704113811000](C:\Users\31330\Pictures\Typora\image-20220704113811000.png)

![image-20220704113823050](C:\Users\31330\Pictures\Typora\image-20220704113823050.png)

同时，亦可获取标签，innerText获取内容（去空格和换行），

innerHtml获取元素加内容，（保留空格和换行）

**案例：密码框显示，隐藏密码**

html

![image-20220704115908427](C:\Users\31330\Pictures\Typora\image-20220704115908427.png)

css

![image-20220704120003894](C:\Users\31330\Pictures\Typora\image-20220704120003894.png)

js

![image-20220704120109188](C:\Users\31330\Pictures\Typora\image-20220704120109188.png)

通过样式属性操作：

![image-20220712222238732](C:\Users\31330\Pictures\Typora\image-20220712222238732.png)

案例：循环精灵图

https://www.bilibili.com/video/BV1Sy4y1C7ha?p=211

![image-20220712224618219](C:\Users\31330\Pictures\Typora\image-20220712224618219.png)

#### DOM核心重点

获取过来的DOM元素是一个对象所以称为**文档对象模型**

![image-20220725203808015](C:\Users\31330\Pictures\Typora\image-20220725203808015.png)

![image-20220725204000304](C:\Users\31330\Pictures\Typora\image-20220725204000304.png)

![image-20220725204013180](C:\Users\31330\Pictures\Typora\image-20220725204013180.png)

![image-20220725204028503](C:\Users\31330\Pictures\Typora\image-20220725204028503.png)

![image-20220725204041703](C:\Users\31330\Pictures\Typora\image-20220725204041703.png)

![image-20220725204119406](C:\Users\31330\Pictures\Typora\image-20220725204119406.png)

![image-20220725204138495](C:\Users\31330\Pictures\Typora\image-20220725204138495.png)

![image-20220725204153170](C:\Users\31330\Pictures\Typora\image-20220725204153170.png)

#### 事件高级

##### 1.注册事件（绑定事件）

注册事件两种方法：传统方式、方法监听注册方式

![image-20220725205047850](C:\Users\31330\Pictures\Typora\image-20220725205047850.png)

``addEventListener``事件监听方式

![image-20220725205212822](C:\Users\31330\Pictures\Typora\image-20220725205212822.png)

##### 2.删除事件（解绑事件）

传统解绑方法：

```html
var divs = document.querySelectorAll('div');
    divs[0].onclick = function() {
        alert(11);
        // 1. 传统方式删除事件
        divs[0].onclick = null;
     }
```

方法监听注册解绑方式：

```html
    // 2. removeEventListener 删除事件
        divs[1].addEventListener('click', fn) // 里面的fn 不需要调用加小括号

        function fn() {
            alert(22);
            divs[1].removeEventListener('click', fn);
        }
```

##### 3.DOM事件流

![image-20220725211809268](C:\Users\31330\Pictures\Typora\image-20220725211809268.png)

![image-20220725212532154](C:\Users\31330\Pictures\Typora\image-20220725212532154.png)

##### 4.事件对象

```html
// 事件对象
var div = document.querySelector('div');
div.onclick = function(e) {
     console.log(e);
    }
     // 1. event 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看
     // 2. 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数
     // 3. 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键
     // 4. 这个事件对象我们可以自己命名 比如 event 、 evt、 e
```

常见属性和方法：

![image-20220725213145564](C:\Users\31330\Pictures\Typora\image-20220725213145564.png)

##### 5.阻止事件冒泡

e.stopPropagation(); // stop 停止  Propagation 传播

```html
<script>
  // 常见事件对象的属性和方法
  // 阻止冒泡  dom 推荐的标准 stopPropagation() 
  var son = document.querySelector('.son');
  son.addEventListener('click', function(e) {
     alert('son');
     e.stopPropagation(); // stop 停止  Propagation 传播
  }, false);
  var father = document.querySelector('.father');
  father.addEventListener('click', function() {
      alert('father');
  }, false);
  document.addEventListener('click', function() {
      alert('document');
  })
</script>
```

##### 6.事件委托

![image-20220725215056718](C:\Users\31330\Pictures\Typora\image-20220725215056718.png)

<img src="C:\Users\31330\Pictures\Typora\image-20220725215201242.png" alt="image-20220725215201242" style="zoom:80%;" />

![image-20220725215238503](C:\Users\31330\Pictures\Typora\image-20220725215238503.png)

##### 7.鼠标事件

![image-20220725215547966](C:\Users\31330\Pictures\Typora\image-20220725215547966.png)

![image-20220725215618639](C:\Users\31330\Pictures\Typora\image-20220725215618639.png)

![image-20220725215824074](C:\Users\31330\Pictures\Typora\image-20220725215824074.png)

```
<script>
    // 1. contextmenu 我们可以禁用右键菜单
    document.addEventListener('contextmenu', function(e) {
        e.preventDefault();
    })
    // 2. 禁止选中文字 selectstart
    document.addEventListener('selectstart', function(e) {
        e.preventDefault();
     })
 </script>
```

##### 8.键盘事件

![image-20220725221221513](C:\Users\31330\Pictures\Typora\image-20220725221221513.png)

***

### BOM

![image-20220726143937871](C:\Users\31330\Pictures\Typora\image-20220726143937871.png)

![image-20220726144355858](C:\Users\31330\Pictures\Typora\image-20220726144355858.png)

![image-20220726144740133](C:\Users\31330\Pictures\Typora\image-20220726144740133.png)

#### window对象常见事件

##### 1.窗口加载事件

![image-20220726145419694](C:\Users\31330\Pictures\Typora\image-20220726145419694.png)

![image-20220726150146383](C:\Users\31330\Pictures\Typora\image-20220726150146383.png)

![image-20220726150242122](C:\Users\31330\Pictures\Typora\image-20220726150242122.png)

// load 等页面内容全部加载完毕，包含页面dom元素 图片 flash  css 等等

 // DOMContentLoaded 是DOM 加载完毕，不包含图片 falsh css 等就可以执行 加载速度比 load更快一些

##### 2.调整窗口大小事件

![image-20220726151626216](C:\Users\31330\Pictures\Typora\image-20220726151626216.png)

#### 定时器

<img src="C:\Users\31330\Pictures\Typora\image-20220726151659709.png" alt="image-20220726151659709" style="zoom:80%;" />

##### 1.``setTimeout()``定时器

![image-20220726151802912](C:\Users\31330\Pictures\Typora\image-20220726151802912.png)

```html
    <script>
        // 1. setTimeout 
        // 语法规范：  window.setTimeout(调用函数, 延时时间);
        // 1. 这个window在调用的时候可以省略
        // 2. 这个延时时间单位是毫秒 但是可以省略，如果省略默认的是0
        // 3. 这个调用函数可以直接写函数 还可以写 函数名 还有一个写法 '函数名()'
        // 4. 页面中可能有很多的定时器，我们经常给定时器加标识符 （名字)
        // setTimeout(function() {
        //     console.log('时间到了');

        // }, 2000);
        function callback() {
            console.log('爆炸了');

        }
        var timer1 = setTimeout(callback, 3000);
        var timer2 = setTimeout(callback, 5000);
        // setTimeout('callback()', 3000); // 我们不提倡这个写法
    </script>
```

![image-20220726152415224](C:\Users\31330\Pictures\Typora\image-20220726152415224.png)

停止``setTimeout()``定时器

![image-20220726152915651](C:\Users\31330\Pictures\Typora\image-20220726152915651.png)

```html
    <button>点击停止定时器</button>
    <script>
        var btn = document.querySelector('button');
        var timer = setTimeout(function() {
            console.log('爆炸了');

        }, 5000);
        btn.addEventListener('click', function() {
            clearTimeout(timer);
        })
    </script>
```

##### 2.``setInterval()``定时器

![image-20220726153226031](C:\Users\31330\Pictures\Typora\image-20220726153226031.png)

```html
    <script>
        // 1. setInterval 
        // 语法规范：  window.setInterval(调用函数, 延时时间);
        setInterval(function() {
            console.log('继续输出');
        }, 1000);
        // 2. setTimeout  延时时间到了，就去调用这个回调函数，只调用一次 就结束了这个定时器
        // 3. setInterval  每隔这个延时时间，就去调用这个回调函数，会调用很多次，重复调用这个函数
    </script>
```

#### JS执行队列

![image-20220726165419927](C:\Users\31330\Pictures\Typora\image-20220726165419927.png)

![image-20220726170649928](C:\Users\31330\Pictures\Typora\image-20220726170649928.png)

![image-20220726170935913](C:\Users\31330\Pictures\Typora\image-20220726170935913.png)

#### location对象

URL

![image-20220726171907706](C:\Users\31330\Pictures\Typora\image-20220726171907706.png)

![image-20220726171934519](C:\Users\31330\Pictures\Typora\image-20220726171934519.png)

![image-20220726173837318](C:\Users\31330\Pictures\Typora\image-20220726173837318.png)

#### navigator对象

![image-20220726174146525](C:\Users\31330\Pictures\Typora\image-20220726174146525.png)

#### history对象

![image-20220726175524173](C:\Users\31330\Pictures\Typora\image-20220726175524173.png)

### PC端网页特效

#### 元素偏移量offset

![image-20220726180321355](C:\Users\31330\Pictures\Typora\image-20220726180321355.png)

#### 元素可视区client

![image-20220726214958544](C:\Users\31330\Pictures\Typora\image-20220726214958544.png)

***

立即执行函数

写法：<img src="C:\Users\31330\Pictures\Typora\image-20220726215733108.png" alt="image-20220726215733108" style="zoom: 67%;" />

***

#### 元素滚动scroll

![image-20220727163943579](C:\Users\31330\Pictures\Typora\image-20220727163943579.png)

***



![image-20220727171222121](C:\Users\31330\Pictures\Typora\image-20220727171222121.png)

***

#### 动画函数封装

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            position: absolute;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
        
        span {
            position: absolute;
            left: 0;
            top: 200px;
            display: block;
            width: 150px;
            height: 150px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div></div>
    <span></span>
    <script>
        // 简单动画函数封装obj目标对象 target 目标位置
        function animate(obj, target) {
            var timer = setInterval(function() {
                if (obj.offsetLeft >= target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(timer);
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';

            }, 3);
        }

        var div = document.querySelector('div');
        var span = document.querySelector('span');
        // 调用函数
        animate(div, 400);
        animate(span, 200);
    </script>
</body>

</html>
```

优化：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            position: absolute;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
        
        span {
            position: absolute;
            left: 0;
            top: 200px;
            display: block;
            width: 150px;
            height: 150px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <button>点击夏雨荷才走</button>
    <div></div>
    <span>夏雨荷</span>
    <script>
        // var obj = {};
        // obj.name = 'andy';
        // 简单动画函数封装obj目标对象 target 目标位置
        // 给不同的元素指定了不同的定时器
        function animate(obj, target) {
            // 当我们不断的点击按钮，这个元素的速度会越来越快，因为开启了太多的定时器
            // 解决方案就是 让我们元素只有一个定时器执行
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function() {
                if (obj.offsetLeft >= target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';

            }, 30);
        }

        var div = document.querySelector('div');
        var span = document.querySelector('span');
        var btn = document.querySelector('button');
        // 调用函数
        animate(div, 300);
        btn.addEventListener('click', function() {
            animate(span, 200);
        })
    </script>
</body>

</html>
```

### 移动端网页特效

https://www.bilibili.com/video/BV1Sy4y1C7ha?p=331&spm_id_from=pageDriver&vd_source=616a9dd528080cf576646147166fe033

#### 触屏事件

```HTML
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        // 1. 获取元素
        // 2. 手指触摸DOM元素事件
        var div = document.querySelector('div');
        div.addEventListener('touchstart', function() {
            console.log('我摸了你');

        });
        // 3. 手指在DOM元素身上移动事件
        div.addEventListener('touchmove', function() {
            console.log('我继续摸');

        });
        // 4. 手指离开DOM元素事件
        div.addEventListener('touchend', function() {
            console.log('轻轻的我走了');

        });
    </script>
</body>

</html>
```

***

### 本地存储

![image-20220728221918076](C:\Users\31330\Pictures\Typora\image-20220728221918076.png)

1.``window.sessionStorage``

一次会话中存在，页面关闭即消失。

<img src="C:\Users\31330\Pictures\Typora\image-20220728222106111.png" alt="image-20220728222106111" style="zoom:67%;" />

<img src="C:\Users\31330\Pictures\Typora\image-20220728222545307.png" alt="image-20220728222545307" style="zoom: 80%;" />

2.``window.localStorage``

<img src="C:\Users\31330\Pictures\Typora\image-20220728223036911.png" alt="image-20220728223036911" style="zoom: 67%;" />

<img src="C:\Users\31330\Pictures\Typora\image-20220728223124366.png" alt="image-20220728223124366" style="zoom: 80%;" />

![image-20220728223346201](C:\Users\31330\Pictures\Typora\image-20220728223346201.png)

***

# jQuery

## 概述

js库：即library，封装好的函数。里面有很多预先封装好的方法。

jQuery就是为了更方便快速操作DOM，里面封装了很多方法，后续用jQuery对象调用这些方法即可。

学习jQuery就是学习调用里面封装的函数，其优化了DOM操作、事件处理、动画设计和Ajax交互。基本兼容了主流浏览器。链式编程、隐式迭代、支持插件拓展开发，轻量、免费、开源。

其宗旨就是：写得少，做的多。

![image-20220730211132828](C:\Users\31330\Pictures\Typora\image-20220730211132828.png)

下载地址：https://jquery.com/

![image-20220730211536641](C:\Users\31330\Pictures\Typora\image-20220730211536641.png)

推荐下载3.X版本。

<img src="C:\Users\31330\Pictures\Typora\image-20220728225459412.png" alt="image-20220728225459412" style="zoom:67%;" />

![image-20220730211830547](C:\Users\31330\Pictures\Typora\image-20220730211830547.png)

点击后直接右键**另存页面为...**即可，最后引入项目中。

## jQuery的基本使用

### 入口函数



```HTML
<body>
    <script>
        // $('div').hide();
        // 1.等着页面DOM加载完毕再去执行js代码
        // $(document).ready(function() {
        //     $('div').hide();
        // })
        // 2.等着页面DOM加载完毕再去执行js代码
        $(function() {
            $('div').hide();
        })
    </script>
    <div>114514</div>
</body>
```

> ```
> $(function() {
>      ......//DOM加载完成的入口(推荐)
> })
> ```
>
> ```
> $(document).ready(function() {
>     ......//DOM加载完成的入口
> })
> ```



![image-20220728230130621](C:\Users\31330\Pictures\Typora\image-20220728230130621.png)

### jQuery的顶级对象：**``$``**

$是*jQuery* 别称，在代码中$和*jQuery* 和等价，为了方便都是$。$是*jQuery* 的顶级对象，相当于原生js中的window，元素通过$包装成*jQuery* 对象，调用*jQuery* 属性和方法。

```HTML
<script>
    // 1. $ 是jQuery的别称（别名）
    // $(function() {
    //     alert(11)
    // });
    //jQuery和$二者可互换，方便起见一般都是$
    jQuery(function() {
        // alert(11)
        // $('div').hide();hide为jQuery封装的方法；
        jQuery('div').hide();
    });
</script>
```

jQuery对象和DOM对象

用原生js获取来的对象是DOM对象，用jQuery方法获取过来的对象是jQuery对象。

jQuery 对DOM的原生方法进行了封装，jQuery 对象只能使用 jQuery 方法，DOM 对象则使用原生的 JavaScirpt 属性和方法。

```HTML
<script>
    //DOM对象，用原生js获取
    var div = document.querySelector('div');
    console.dir(div);
    // $('div')是一个jQuery 对象
    $('div'); 
    console.dir($('div'));
</script>
```

控制台输出：

![image-20220730203313022](C:\Users\31330\Pictures\Typora\image-20220730203313022.png)

> jQuery 对象只能使用 jQuery 方法：例如
>
> 衔接上述代码：``div.style.display='none';``//是原生js方法，DOM对象可调用
>
> 但：``$('div').style.display='none';``//这句代码就是错的，jQuery 对象只能使用jQuery 封装的方法。
>
> 所以，jQuery 只是对js常用属性和方法进行了封装。DOM使用原生js方法和属性，jQuery 使用jQuery 属性和方法。

### jQuery 对象和DOM对象相互转换

jQuery 转化为DOM(两种方法)：

1. $('div')[index];//index是索引号
2. $('div').get(index);

```
<script>
    var div = document.querySelector('div');
    $('div')[0].hide()
    $('div').get(0).hide()
</script>
```

DOM转化为*jQuery* ：

```
//直接获取元素即可
$('div');
```

## jQuery常用API

### jQuery选择器

1. jQuery 基础选择器

原生 JS 获取元素方式很多，很杂，而且兼容性情况不一致，因此 jQuery 给我们做了封装，使获取元素统一标准。

```java
$(“选择器”) //里面选择器直接写 CSS 选择器即可，但是要加引号
```

获取方式与原生js无异：

![image-20220730214338985](C:\Users\31330\Pictures\Typora\image-20220730214338985.png)

2. jQuery 层级选择器

![image-20220730214457746](C:\Users\31330\Pictures\Typora\image-20220730214457746.png)

jQuery设置样式的方法：

```java
$('div').css('属性', '值')
```

for instance：(Set the color for all the LI under UL)

```java
$("ul li").css("color", "red");
```

隐式迭代：遍历内部 DOM 元素（伪数组形式存储）的过程。

例如：给UL里的很多LI都设置成红色字体

直接$("ul li").css("color", "red");//隐式迭代自动遍历每一个LI。

3. jQuery 筛选选择器

![image-20220730215518712](C:\Users\31330\Pictures\Typora\image-20220730215518712.png)

for instance：(Get the first LI under UL)

```java
$("ul li:first").css("color", "red");
```

**jQuery 筛选方法**



![image-20220730215946204](C:\Users\31330\Pictures\Typora\image-20220730215946204.png)

重点记住：

`` parent()//找亲爸 `` ；``parents('名称')//找指定祖先``

`` children()//找亲儿子（可以是多个）``

`` find()//找后代`` 

``  siblings()//找兄弟``  

`` eq()``//精确查找第几个儿子，从0开始



> Element Traversal API为DOM元素添加了下面5个属性：
>
> - `childElementCount`：返回子元素（不包括文本节点和注释）的个数。
> - `firstElementChild`：指向第一个子元素。
> - `lastElementChild`：指向最后一个子元素。
> - `previousElementSibling`：指向前一个同辈元素。
> - `nextElementSibling`：指向后一个同辈元素。



***

### jQuery 样式操作



#### 操作CSS方法

jQuery 可以使用 css 方法来修改简单元素样式。

>- 参数只写属性名，则是返回属性值
>
>```
>$(this).css(''color'');
>```

>- 参数是**属性名，属性值，逗号分隔**，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号
>
>```
>$(this).css(''color'', ''red'');
>```

>- 参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开， 属性可以不用加引号(对象写法，可以不带引号)
>
>```
>$(this).css({
>    "width": "400px",
>    height: 400,
>    "color":"white",
>    "font-size":"20px"
>});
>```



#### 设置类样式方法

作用等同于以前的 classList，可以操作类样式， 注意操作类里面的参数不要加点。

> - 添加类
>
> ```java
> $(“div”).addClass(''example'');
> ```

> - 移除类
>
> ```java
> $(“div”).removeClass(''example'');
> ```

> - 切换类
>
> ```java
> $(“div”).toggleClass(''example'');
> ```

> ==Attention:类操作与className区别==
>
> 原生 JS 中 className 会覆盖元素原先里面的类名。
> jQuery 里面类操作只是对指定类进行操作，不影响原先的类名。

### jQuery 效果

可在API文档中查询具体用法：[https://jquery.cuishifeng.cn/](https://jquery.cuishifeng.cn/)

jQuery 封装了很多动画效果，例如：

![image-20220801182932251](C:\Users\31330\Pictures\Typora\image-20220801182932251.png)

#### 1.显示隐藏效果



```java
1.显示
//（1）speed:字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
//（2）easing:(Optional)用来指定切换效果，默认是“swing”，可用参数“linear”。
//（3）fn:回调函数，在动画完成时执行的函数，每个元素执行一次。
show([speed,[easing],[fn]]);//中括号表示可以省略此参数，无动画直接显示
```

```java
2.隐藏
//（1）speed:字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
//（2）easing:(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
//（3）fn:回调函数，在动画完成时执行的函数，每个元素执行一次
hide([speed,[easing],[fn]]);//中括号表示可以省略此参数，无动画直接显示
```

```java
3.切换显示和隐藏
toggle([speed,[easing],[fn]];
```

![](C:\Users\31330\Pictures\Typora\4-16593607124061.gif)

#### 2.滑动效果

参数意思与显示隐藏参数一致

```javascript
1.下滑
slideDown([speed,[easing],[fn]];
```

```javascript
2.上滑
slideUp([speed,[easing],[fn]];
```

```javascript
3.滑动切换
slideToggle([speed,[easing],[fn]];
```

==**事件切换**==

```java
//（1）over:鼠标移到元素上要触发的函数（相当于mouseenter）
//（2）out:鼠标移出元素要触发的函数（相当于mouseleave）
//（3）如果只写一个函数，则鼠标经过和离开都会触发它
hover([over,]out);
```

for instance:(The drop-down menu of the navigation bar).

实现效果：

![](C:\Users\31330\Pictures\Typora\2.gif)

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        li {
            list-style-type: none;
        }
        
        a {
            text-decoration: none;
            font-size: 14px;
        }
        
        .nav {
            margin: 0 auto;
            height: 40px;
            border-bottom: 1px solid red;
        }
        
        .nav>li {
            position: relative;
            float: left;
            width: 80px;
            height: 41px;
            text-align: center;
        }
        
        .nav li a {
            display: block;
            width: 100%;
            height: 100%;
            line-height: 41px;
            color: #333;
        }
        
        .nav>li>a:hover {
            background-color: #eee;
        }
        
        .nav ul {
            display: none;
            position: absolute;
            top: 41px;
            left: 0;
            width: 100%;
            border-left: 1px solid red;
            border-right: 1px solid red;
        }
        
        .nav ul li {
            border-bottom: 1px solid red;
        }
        
        .nav ul li a:hover {
            background-color: #FFF5DA;
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <ul class="nav">
        <li>
            <a href="#">导航一</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">导航二</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">导航三</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">导航四</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
    </ul>
    <script>
        $(function() {
            
            ......
        })
    </script>
</body>

</html>
```

jQuery部分有多种写法：

> 1. 上滑和下滑分别用鼠标离开和经过来实现
>
> ```javascript
> //鼠标经过，下滑
> $(".nav>li").mouseover(function() {
>     $(this).children("ul").slideDown(200);
> });
> //鼠标离开，上滑
> $(".nav>li").mouseout(function() {
>     $(this).children("ul").slideUp(200);
> });
> ```
>
> 2. 用上面说的事件切换来写
>
> ```javascript
> //事件切换 hover 就是鼠标经过和离开的复合写法，两个函数对应经过和离开。
> $(".nav>li").hover(function() {
>     $(this).children("ul").slideDown(200);
> }, function() {
>     $(this).children("ul").slideUp(200);
> });
> ```
>
> 简化事件切换写法：只写一个函数，鼠标经过和鼠标离开都会触发这个函数
>
> ```javascript
> $(".nav>li").hover(function() {
>     $(this).children("ul").slideToggle();
> });
> ```

上述写法的bug：快速经过离开，导航动画等一个结束，另一个才开始

![](C:\Users\31330\Pictures\Typora\3.gif)



待解决：动画队列（动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。）

解决方法：**停止排队**

```javascript
//(1)stop()方法用于停止动画或效果。
//(2)注意:stop()写到动画或者效果的前面，相当于停止结束上一次的动画。只执行最新的一次。
stop();
```

完整代码：

```javascript
$(".nav>li").hover(function() {
    // stop 方法必须写到动画的前面，结束上一次的动画
    $(this).children("ul").stop().slideToggle();
});
```

#### 3.淡入淡出效果

就是透明度从0增加到1的变化。

//参数与上述一致

（1）speed：字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
（2）easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
（3）fn:  回调函数，在动画完成时执行的函数，每个元素执行一次。

```java
1.淡入
fadeIn([speed,[easing],[fn]];
```

```java
2.淡出
fadeOut([speed,[easing],[fn]];
```

```java
3.淡入淡出切换
fadeToggle([speed,[easing],[fn]];
```

**渐进方式调整到指定的不透明度**

```java
//opacity 透明度，取值0~1
fadeTo([[speed],opacity,[easing],[fn]];
```

#### 4.自定义动画 animate

```java
//params: 想要更改的样式属性，以对象形式传递。属性名可以不用带引号，如果是复合属性则需要采
取驼峰命名法 borderLeft。其余参数都可以省略。
animate(params,[speed],[easing],[fn];
```



***

### jQuery 属性操作



#### 设置或获取元素固有属性值

元素固有属性就是元素本身自带的属性，比如 <a> 元素里面的 href ，比如 <input> 元素里面的 type。

```java
1.获取
prop(''属性'');
2.设置
prop(''属性'', ''属性值'');
```



#### 设置或获取元素自定义属性值

用户自己给元素添加的属性，我们称为自定义属性。 比如给 div 添加 index =“1”。

```java
1.获取
attr(''属性'');  // 类似原生 getAttribute()
2.设置
attr(''属性'', ''属性值'');   // 类似原生 setAttribute()
```



**数据缓存data()**

data() 方法可以在指定的元素上存取数据，并不会修改 DOM 元素结构。本质上是存放在元素缓存中，一旦页面刷新，之前存放的数据都将被移除。

```java
1.存入数据
data(''name'',''value'');   // 向被选元素附加数据
//例如：$('span').data('uname','roydon');
2.获取数据
date(''name'');  //得到数字型数据，获取H5自定义属性data-index时，直接写index即可
```



***

### jQuery 内容文本值

主要针对元素的内容还有表单的值操作。

1. 普通元素内容 html()（ 相当于原生inner HTML)

```java
1.获取元素内容
html()
2.设置元素内容
html(''内容'')
```

2. 普通元素文本内容 text()   (相当与原生 innerText)

```java
1.获取
text()
2.设置
text(''文本内容'')
```

3. 表单的值 val()（ 相当于原生value)

```
1.获取
val()
2.设置
val(''内容'')
```

保留两位小数：``toFixed(2);``

***

### jQuery 元素操作

#### 遍历元素

jQuery 隐式迭代只能对同一类元素进行相同操作。

遍历元素可以做到给每个元素添加不同操作。

**语法1：**

```javascript
//index 元素索引号
//domEle 是每个DOM元素对象（非jquery对象）；所以要想使用jquery方法，需要将这个dom元素转换为jquery对象 $(domEle)
$("div").each(function (index, domEle) {
    ......
});
```

例如：统计三个div内容的和

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>HTML5</title>
    <script src="./jquery.min.js"></script>
    <script>
        $(function () {
            var sum = 0;
            $('div').each(function (index, domEle) {
                console.log(index);
                console.log(domEle);
                sum += parseInt($(domEle).text());
            })
            console.log(sum);
        })
    </script>
</head>

<body>
    <div>2</div>
    <div>3</div>
    <div>5</div>
</body>

</html>
```

结果：

<img src="C:\Users\31330\Pictures\Typora\image-20220802185810609.png" alt="image-20220802185810609" style="zoom:80%;" />

**语法2：**

```javascript
//$.each()方法可用于遍历任何对象。主要用于数据处理，比如数组，对象
//index 元素索引号;element 遍历内容
$.each(object，function (index, element) {
    ......
});
```

例如：遍历对象{name:"roydon",age:20}

```javascript
$(function () {
    var user = { name: "roydon", age: 20 };
    $.each(user, function (i, ele) {
    //i 为属性名；ele 为属性值。遍历数组时i 为下标；ele 为值
        console.log(i + " : " + ele);
    })
})
```

结果：

![image-20220802190354543](C:\Users\31330\Pictures\Typora\image-20220802190354543.png)



***

#### 创建元素

```java
$(''<li></li>''); 
```

***

#### 添加元素

```javascript
1.内部添加（添加过后与原元素程父子关系
element.append(''内容'');//把内容放入匹配元素内部最后面，类似原生 appendChild。
element.prepend(''内容'');//把内容放入匹配元素内部最前面。
```

```javascript
2.外部添加（添加过后与原元素程兄弟关系
element.after(''内容'');//把内容放入目标元素后面
element.before(''内容'');//把内容放入目标元素前面
```

***

#### 删除元素

```javascript
element.remove();//删除匹配的元素（本身）
element.empty();//删除匹配的元素集合中所有的子节点
element.html('''');//清空匹配的元素内容，也可设置内容
```

例如：元素如下：

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

1.$("ul").remove();  结果：ul连同li全部被删除

2.$("ul").empty();  结果：清空ul里所有的li；.html('''');与其类似

***

### jQuery 尺寸、位置操作

#### jQuery 尺寸

![image-20220803184045483](C:\Users\31330\Pictures\Typora\image-20220803184045483.png)

参数为空时是取值，参数不为空是设置宽高；

例如：

```
$("div").width();//获取div宽度
$("div").width(300);//设置宽300
```

#### jQuery 位置

位置主要有三个： offset()、position()、scrollTop()/scrollLeft()

1.offset() 设置或获取元素偏移

- offset() 相对于文档的偏移坐标，跟父级没有关系。
- 该方法有2个属性 left、top 。offset().top  获取距离文档顶部的距离，offset().left 获取距离文档左侧的距离。
- 可以设置元素的偏移：offset({ top: 50, left: 50 });

2.position() 获取元素偏移

- position() 返回被选元素相对于带有定位的父级偏移坐标，如果父级都没有定位，则以文档为准。
- 该方法有2个属性 left、top。position().top 获取距离定位父级顶部的距离，position().left 获取距离定位父级左侧的距离。
- 该方法只能获取。

3.scrollTop()/scrollLeft() 设置或获取元素被卷去的头部和左侧

- 类似于一个小盒子放大图片，图片会显示不全，不全的部分就是scrollTop()/scrollLeft()

- 加参数表示设置

***

## jQuery 事件

***

### jQuery 事件注册

事件和原生基本一致。

比如mouseover、mouseout、blur、focus、change、keydown、keyup、resize、scroll(页面滚动) 等

常用事件：[http://www.htmleaf.com/jquery-doc/#events](http://www.htmleaf.com/jquery-doc/#events)

![image-20220926134221444](C:\Users\31330\Pictures\Typora\image-20220926134221444.png)

**语法：**

```javascript
element.事件(function(){})
例如：
$(“div”).click(function(){
    //事件处理程序
})
```

***

### jQuery 事件处理

1.事件处理 **on()** 绑定事件在匹配元素上绑定**一个或多个事件**的事件处理函数。

```javascript
//1. events: 一个或多个用空格分隔的事件类型，如"click"或"mouseover" 。
//2. selector: 元素的子元素选择器。
//3. fn:回调函数 即绑定在元素身上的侦听函数。
element.on(events,[selector],fn);
```

🔸当**on()**绑定多个事件：

```javascript
$(“div”).on({
    mouseover: function(){}, //事件1
    mouseout: function(){},  //事件2
    click: function(){}      //事件3
});
//若mouseover事件和mouseout事件响应程序相同，则空格隔开写一起
//$(“div”).on(“mouseover mouseout”, function() {
//    ......
//});
```

🔸事件委派：

```javascript
//li的处理事件委派给父ul，里面每个li都有了click
$('ul').on('click', 'li', function() {
    alert('hello world!');
});
```

==注意：==事件委派（事件代理）现在大多采用这种写法：

当动态创建元素时，可以动态自动为其绑定事件

```javascript
例如：ol里添加li并动态绑定事件
$("ol").on("click", "li", function() {
    alert('hello world!');
})
var li = $("<li>后来创建的li</li>");
$("ol").append(li);
//如果此时用传统的绑定事件绑定单个li，则不会生效。
//一般对于后续拼接元素的案例，都是用事件委派（事件代理）
```

2.事件处理 **off()** 解绑事件可以移除通过 on() 方法添加的事件处理程序。

当只想让事件触发一次，就会用到解绑事件。（也可以把绑定事件的on()改为one()表示事件只触发一次）

```javascript
$("p").off(); // 解绑p元素所有事件处理程序
$("p").off( "click");  // 解绑p元素上面的点击事件
$("ul").off("click", "li");  // 解绑事件委托
```

3.自动触发事件 **trigger()** 

有些事件希望自动触发, 比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发。

例如，div自动触发点击事件：

```javascript
$(function() {
    $("div").on("click", function() {
        $(this).css("background","red")
    });
    // 自动触发点击事件
    // 方法一： 元素.事件()
    // $("div").click();会触发元素的默认行为
    // 方法二： 元素.trigger("事件")
    // $("div").trigger("click");会触发元素的默认行为
    // 方法三： 元素.triggerHandler("事件") 就是不会触发元素的默认行为
    $("div").triggerHandler("click");
});
```

***

### jQuery 事件对象

事件被触发，就会有事件对象event的产生。

```javascript
element.on(events,[selector],function(event) {
    //阻止默认行为：event.preventDefault()  或者 return false;
    //阻止冒泡： event.stopPropagation()
})
```

***

## jQuery 其它方法

***

### jQuery 对象拷贝

把某个对象拷贝（合并） 给另外一个对象使用:

```javascript
//(1)deep: 如果设为true 为深拷贝，默认为false 浅拷贝
//(2)target 目标对象
//(3)object1 待拷贝对象；；objectN:待拷贝到第N个对象的对象。
$.extend([deep], target, object1, [objectN]));
```



> 🔸浅拷贝：
>
> 把原对象中**复杂数据类型**的``地址``拷贝给目标对象；
>
> 修改目标对象会影响被拷贝对象：若修改拷贝后对象复杂数据类型的值原对象也会被修改
>
> 现在js的深拷贝可以用 ``new = {...oldObj}``
>
> 🔸深拷贝：
>
> 完全拷贝；
>
> 修改目标对象不会影响被拷贝对象

### jQuery 多库共存

jQuery使用$作为标示符，随着jQuery的流行,其他 js 库也会用这$作为标识符， 这样一起使用会引起冲突。故需要一个解决方案，让jQuery 和其他的js库不存在冲突，可以同时存在，这就叫做多库共存。

> 解决：
>
> 1. 把里面的 $ 符号 统一改为 jQuery。 比如  jQuery(''div'');
> 2. jQuery 变量规定新的名称：$.noConflict();  比如 var xx = $.noConflict();

### js的五种迭代方法

ECMAScript5为数组定义了5个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象（即影响this的值）。传入这些方法中的函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。根据使用方法的不同，这个函数执行后的返回值可能会也可能不会影响方法的返回值。这5个迭代方法是：

- `every()`：对数组中的每一项运行给定的函数。如果该函数对每一项都返回`true`，则返回`true`。
- `filter()`：对数组中的每一项运行给定的函数，返回该函数会返回`true`的项组成的数组。
- `forEach()`：对数组中的每一项运行给定的函数。该方法没有返回值。
- `map()`：对数组中的每一项运行给定的函数，返回每次函数调用的结果组成的数组。
- `some()`：对数组中的每一项运行给定的函数，如果该函数对任一项返回`true`，则返回`true`。

***

**`every()`**和**`some()`**非常相似，它们都用于查询数组中的项是否满足某个条件。对于`every()`方法来说，传入的函数必须对每一项都返回`true`，这个方法才返回`true`。否则，它就返回`false`。而`some()`方法则是只要传入的函数对数组的某一项返回`true`，就会返回`true`。例如：

```javascript
var nums = [1,2,3,4,5,4,3,2,1];
var result = nums.every(function(item, index, array){
  return (item > 2);
})
console.info(result);
// 控制台中打印 false
```

```javascript
var nums = [1,2,3,4,5,4,3,2,1];
var result = nums.some(function(item, index, array){
  return (item > 2);
})
console.info(result);
// 控制台中打印 true
```

**`filter()`**函数，它利用指定的函数确定是否存在返回的数组中包含某一项。例如，要返回一个所有数值都大于2的数组，可以使用下面的代码：

```javascript
var nums = [1,2,3,4,5,4,3,2,1];
var result = nums.filter(function(item, index, array){
  return (item > 2);
})
console.info(result);
// [3,4,5,4,3]
```

**`map()`**方法也**返回一个数组**，而这个数组的每一项都是在原始数组中的对应项上运行传入函数的结果。例如，可以给数组中的每一项都乘以2，然后返回这些乘积组成的数组：

```javascript
var nums = [1,2,3,4,5,4,3,2,1];
var result = nums.map(function(item, index, array){
  return item * 2;
})
console.info(result);
// [2,4,6,8,10,8,6,4,2]
```

**`forEach()`**方法，它只是对数组中的每一项运行传入的函数。这个方法**没有返回值**，本质上于使用`for`循环迭代数组是一样的。看下面的例子：

```javascript
var nums = [1,2,3,4,5,4,3,2,1];
nums.forEach(function(item, index, array){
  //执行需要的操作
})
```







***

### jQuery 插件

jQuery 功能比较有限，想要更复杂的特效效果，可以借助于 jQuery 插件完成。
注意: 这些插件也是依赖于jQuery来完成的，所以必须要先引入jQuery文件，因此也称为 jQuery 插件。
jQuery 插件常用的网站：

1. jQuery 插件库 http://www.jq22.com/ 

2. jQuery 之家 http://www.htmleaf.com/  

jQuery 插件使用步骤：

1. 引入相关文件。（jQuery 文件 和 插件文件） 
2. 复制相关html、css、js (调用插件)。

jQuery 插件演示：
\1. 瀑布流
\2. 图片懒加载（图片使用延迟加载在可提高网页下载速度。它也能帮助减轻服务器负载）
当我们页面滑动到可视区域，再显示图片。
我们使用jquery 插件库 EasyLazyload。 注意，此时的js引入文件和js调用必须写到 DOM元素（图片）最后面
\3. 全屏滚动（fullpage.js）
gitHub： https://github.com/alvarotrigo/fullPage.js
中文翻译网站： http://www.dowebok.com/demo/2014/77/





https://www.bilibili.com/video/BV1Sy4y1C7ha?p=435&spm_id_from=pageDriver&vd_source=616a9dd528080cf576646147166fe033





***

# Ajax

***

## 基础



### URL地址

统一资源定位符，网页资源统一标识符。

![image-20220804180332284](C:\Users\31330\Pictures\Typora\image-20220804180332284.png)

### 客户端和服务器通信过程 

![image-20220804180805856](C:\Users\31330\Pictures\Typora\image-20220804180805856.png)

浏览器开发工具分析通信过程

![image-20220804181231618](C:\Users\31330\Pictures\Typora\image-20220804181231618.png)

HTML是网页的骨架
 CSS是网页的颜值
 Javascript是网页的行为

**数据，则是网页的灵魂**

![image-20220804181647542](C:\Users\31330\Pictures\Typora\image-20220804181647542.png)

![image-20220804182156982](C:\Users\31330\Pictures\Typora\image-20220804182156982.png)

客户端请求服务器时，请求的方式有很多种，最常见的两种请求方式分别为 get 和 post 请求。
 get 请求通常用于获取服务端资源（向服务器要资源）
      例如：根据 URL 地址，从服务器获取 HTML 文件、css 文件、js文件、图片文件、数据资源等

 post 请求通常用于向服务器提交数据（往服务器发送资源）
      例如：登录时向服务器提交的登录信息、注册时向服务器提交的注册信息、添加用户时向服务器提交的用户信息等各种数据提交操作

### 接口

请求数据时，被请求的 URL 地址，就叫做数据接口（简称接口）。

同时，每个接口必须有请求方式。具体需要哪些操作可查看接口文档。

接口测试工具：（好处：不用写代码）

<img src="C:\Users\31330\Pictures\Typora\image-20220804185827556.png" alt="image-20220804185827556" style="zoom: 80%;" />

PostMan下载地址：[https://www.postman.com/downloads/](https://www.postman.com/downloads/)

或中文版工具apifox：https://www.apifox.cn/

中文版工具apifox帮助地址：[帮助中心 | Apifox 使用文档](https://www.apifox.cn/help/)

<img src="C:\Users\31330\Pictures\Typora\apifox-logo-text.png" alt="img" style="zoom: 50%;" />

### 初识Ajax 

全称是 Asynchronous Javascript And XML（异步 JavaScript 和 XML）。
通俗的理解：在网页中利用 XMLHttpRequest 对象和服务器进行数据交互的方式，就是Ajax。

Ajax能让我们轻松实现网页与服务器之间的数据交互。

应用场景：

- 注册用户时动态检测用户名是否被占用
- 搜索提示列表
- 数据分页显示
- 数据的增删改查

## jQuery中的Ajax

由于浏览器中提供的 XMLHttpRequest 用法比较复杂。

所以 jQuery 对 XMLHttpRequest 进行了封装，提供了一系列 Ajax 相关的函数，极大地降低了 Ajax 的使用难度。

jQuery 中发起 Ajax 请求最常用的三个方法如下：

>1.   **$.get()**
>2.   **$.post()**
>3.   **$.ajax()**



1、``$.get()``

功能单一，发起 get 请求，从服务器拿数据。

```javascript
$.get(url, [data], [callback])
//参数一：url	string类型	要请求的资源地址
//参数二：data	object类型	请求资源期间要携带的参数
//参数三：callback	请求成功时的回调函数
```

2、``$.post()``

功能单一，发起 post 请求，向服务器提交数据。

```javascript
$.post(url, [data], [callback]);
//参数一：url	string类型	提交数据的地址
//参数二：data	object类型	要提交的数据
//参数三：callback	数据提交成功时的回调函数
```

3、``$.ajax()``

功能更多

```javascript
$.ajax({
   type: '', // 请求的方式 GET 或 POST
   url: '',  // 请求的URL
   data: { },// 请求要携带的数据
   success: function(res) { } // 请求成功之后的回调函数
})
```



添加删除图书：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <link rel="stylesheet" href="./lib/bootstrap.css" />
  <script src="./lib/jquery.js"></script>
</head>

<body style="padding: 20px;">

  <!-- 添加图书的Panel面板 bs3 -->
  <div class="panel panel-primary">
    <div class="panel-heading">
      <h3 class="panel-title">添加新图书</h3>
    </div>
    <div class="panel-body form-inline">

      <div class="input-group">
        <div class="input-group-addon">书名</div>
        <input type="text" class="form-control" id="iptBookname" placeholder="请输入书名">
      </div>

      <div class="input-group">
        <div class="input-group-addon">作者</div>
        <input type="text" class="form-control" id="iptAuthor" placeholder="请输入作者">
      </div>

      <div class="input-group">
        <div class="input-group-addon">出版社</div>
        <input type="text" class="form-control" id="iptPublisher" placeholder="请输入出版社">
      </div>

      <button id="btnAdd" class="btn btn-primary">添加</button>

    </div>
  </div>


  <!-- 图书的表格 -->
  <table class="table table-bordered table-hover">
    <thead>
      <tr>
        <th>Id</th>
        <th>书名</th>
        <th>作者</th>
        <th>出版社</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody id="tb"></tbody>
  </table>

  <script>
    $(function () {
      /* 从接口获取数据 */
      function getBooks() {
        $.get('http://www.liulongbin.top:3006/api/getbooks', function (res) {
          console.log(res);
          if (res.status !== 200) return alert('false')
          var items = new Array();
          $.each(res.data, function (i, ele) {
            console.log(i+"->"+ele.id + "-" + ele.bookname + "-" + ele.author + "-" + ele.publisher);
            items.push('<tr><td>' + ele.id + '</td><td>' + ele.bookname + '</td><td>' + ele.author + '</td><td>' + ele.publisher + '</td><td><a href="javascript:;" class="del" data-id="' + ele.id + '">删除</a></td></tr>')
          })
          $('#tb').empty().append(items.join(''))
        })
      }
      getBooks()
      // $('.del').on('click', function () {
      //   console.log('hello del');
      // })
      /* 动态创建元素，需要事件委派绑定事件 */
      $('#tb').on('click', '.del', function () {
        console.log('del')
        var id = $(this).data('id')
        console.log(id);
        /* 根据id删除一条数据 */
        $.get('http://www.liulongbin.top:3006/api/delbook', { id: id }, function (res) {
          if (res.status !== 200) return alert('false')
          getBooks()
        })
      })

      /* 新增数据 */
      $('#btnAdd').on('click', function () {

        var iptBookname = $('#iptBookname').val().trim()
        var iptAuthor = $('#iptAuthor').val().trim()
        var iptPublisher = $('#iptPublisher').val().trim()
        if (iptBookname.length <= 0 || iptAuthor.length <= 0 || iptPublisher.length <= 0) return alert('不能为空！')
        var newBook = {
          bookname: iptBookname,
          author: iptAuthor,
          publisher: iptPublisher
        }
        $.post('http://www.liulongbin.top:3006/api/addbook', newBook, function (res) {
          if (res.status !== 201) return alert('false')
          getBooks()
          $('#iptBookname').val('')
          $('#iptAuthor').val('')
          $('#iptPublisher').val('')
        })
      })
    })
  </script>
 
</body>

</html>
```



***

## form表单与模板引擎

### form表单

表单就是提交数据到服务器的采集工具。HTML中的``form``标签，就是用于采集用户输入的信息，并通过``form``标签的提交操作，把采集到的信息提交到服务器端进行处理。

表单由三个基本部分组成：

![image-20220805153113906](C:\Users\31330\Pictures\Typora\image-20220805153113906.png)

>🟥：``form``表单标签
>
>🟩：表单域。包含了文本框、密码框、隐藏域、多行文本框、复选框、单选框、下拉选择框和文件上传框等。
>
>🟦：表单按钮

**``form``标签的属性:**

1、**action**:

提交表单时，向何处发送表单数据。
值是 URL 地址，这个 URL 专门负责接收表单提交过来的数据。
当 ``form`` 表单在未指定 action 属性值的情况下，action 的默认值为当前页面的 URL 地址。

提交表单后，页面会跳转到 action 属性指定的 URL 地址

2、**target**:

在何处打开action URL。

默认情况下，target 的值是 _self，表示在相同的框架中打开 action URL。

|   **值**    | **描述**                       |
| :---------: | :----------------------------- |
|   _blank    | 在新窗口中打开。               |
|    _self    | 在相同的窗口中打开。（默认）   |
|   _parent   | 在父框架集中打开。（很少用）   |
|    _top     | 在整个窗口中打开。（很少用）   |
| *framename* | 在指定的框架中打开。（很少用） |

3、**method**:

method 属性规定以何种方式把表单数据提交到 action URL。
可选值有两个： get(默认) 和 post。

🔸**注意：**
get 方式适合用来提交**少量的、简单的**数据。
post 方式适合用来提交**大量的、复杂的、或包含文件上传**的数据。
实际开发中，``form`` 表单的 post 提交方式用的最多，很少用 get。例如登录、注册、添加数据等表单操作，都需要使用 post 方式来提交表单。

4、enctype

规定在发送表单数据之前如何对数据进行编码。

可选值有三个，默认情况下enctype 的值为 application/x-www-form-urlencoded，表示在发送前编码所有的字符。

|              **值**               | **描述**                                                     |
| :-------------------------------: | ------------------------------------------------------------ |
| application/x-www-form-urlencoded | 在发送前编码所有字符（默认）                                 |
|        multipart/form-data        | 不对字符编码。 在使用包含文件上传控件的表单时，必须使用该值。 |
|            text/plain             | 空格转换为 “+” 加号，但不对特殊字符编码。（很少用）          |

🔸**注意：**
在涉及到**文件上传**的操作时，必须将 enctype 的值设置为 **multipart/form-data**
如果表单的提交不涉及到文件上传操作，不用加此属性就行。

***

==表单的同步提交==

通过点击 submit 按钮，触发表单提交的操作，从而使页面跳转到 action URL 的行为，叫做表单的同步提交。

**缺点：**

>1.表单同步提交后，**整个页面会发生跳转**，跳转到 action URL 所指向的地址，用户体验差。
>2.表单同步提交后，**页面之前的状态和数据会丢失**。

**解决：**

> 表单只负责采集数据，Ajax 负责将数据提交到服务器。

***

### Ajax提交表单数据

监听表单提交事件：

```javascript
//方法一：
$('#form1').submit(function(e) {
   alert('监听到了表单的提交事件')
})
//方法二：
$('#form1').on('submit', function(e) {
   alert('监听到了表单的提交事件')
})
```

阻止表单默认提交行为：``event.preventDefault()``

```javascript
$('#form1').submit(function(e) {
   // 阻止表单提交和页面跳转
   e.preventDefault()
})

$('#form1').on('submit', function(e) {
   // 阻止表单提交和页面跳转
   e.preventDefault()
})
```

获取表单数据:

jQuery 提供的 **serialize()** 函数，可以一次性获取表单中所有数据。使用 **serialize() **时，必须每个表单元素添加 name 属性。

例如：表单如下

```
<form id="form1">
    <input type="text" name="name" />
    <input type="password" name="password" />
    <button type="submit">提交</button>
</form>
```

**serialize()** 函数获取数据：

```
$('#form1').serialize()
// 数据：
// name=值&password=值
```

***

### 模板引擎

渲染UI结构时遇到的问题，需要拼接的元素太长，结构比较复杂：

```javascript
li.push('<li class="list-group-item">'+ item.content +'<span class="badge cmt-date">评论时间：'+ item.time +'</span><span class="badge cmt-person">评论人：'+ item.username +'</span></li>')
```

模板引擎，就是程序员指定的模板结构和数据。

定义HTML页面，然后js提供数据。

**art-template模板引擎**：

网址：[ http://aui.github.io/art-template/zh-cn/index.html]( http://aui.github.io/art-template/zh-cn/index.html)

下载js文件：http://aui.github.io/art-template/zh-cn/docs/installation.html

![image-20220806193718182](C:\Users\31330\Pictures\Typora\image-20220806193718182.png)

使用模板引擎步骤：

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>模板引擎</title>
  <!-- 1. 导入模板引擎template-web.js文件 -->
  <script src="./lib/template-web.js"></script>
  <script src="./lib/jquery.js"></script>
</head>

<body>

  <div id="container"></div>

  <!-- 2. 定义模板，在script中定义的HTML需要指定html解析type="text/html" -->
  <script type="text/html" id="example">
  	<!-- {{}}表示占位符，是要传入的数据 -->
    <h1>{{name}}</h1>
  </script>

  <script>
    // 3. 取出数据
    var data = { name: 'roydon' }
    // 4. 调用模板引擎提供的 template 函数（第一个参数表示模板的id，第二个参数是数据）
    var temp = template('example', data)
    // 5. 渲染HTML
    $('#container').html(temp)
  </script>
  
</body>

</html>
```

**art-template标准语法**：

art-template 提供了 {{ }} 这种语法格式，在 {{ }} 内可以进行变量输出，或循环数组等操作，这种 {{ }} 语法在 art-template 中被称为标准语法。

```javascript
{{value}}
{{obj.key}}//对象属性的输出
{{obj['key']}}//对象属性的输出
{{a ? b : c}}//三元表达式
{{a || b}}//逻辑
{{a + b}}//运算
//若数据值包含HTML结构需要完整输出且被渲染，则：
{{@ value }}
```

条件输出：

```
{{if condition}} 按需输出的内容 {{/if}}
{{if condition1}} 按需输出的内容 {{else if condition2}} 按需输出的内容 {{/if}}
```

![image-20220806200717353](C:\Users\31330\Pictures\Typora\image-20220806200717353.png)

循环输出：

```javascript
{{each arr}}
    {{$index}} {{$value}}
{{/each}}
```

例如输出数组：{ arr: ['1', '2', '3'] }

```javascript
<ul>
  {{each arr}}
  <li>索引:{{$index}}值:{{$value}}</li>
  {{/each}}
</ul>
```

过滤器

```javascript
{{value | filterName}}
//定义过滤器，过滤器名称filterName
template.defaults.imports.filterName = function(value){
    /*return处理的结果*/
}
```



***

实现原理：

 **正则与字符串操作**：

**exec()** 函数用于检索字符串中的正则表达式的匹配。
如果字符串中有匹配的值，则返回该匹配值，否则返回 null。

例如：

```javascript
var str = 'hello'
var pattern = /o/                         
// 输出的结果["o", index: 4, input: "hello", groups: undefined]
console.log(pattern.exec(str)) 
```

正则表达式中 ( ) 包起来的内容表示一个分组，可以通过分组来提取自己想要的内容，示例代码如下：

```javascript
 var str = '<div>我是{{name}}</div>'
 var pattern = /{{([a-zA-Z]+)}}/

 var patternResult = pattern.exec(str)
 console.log(patternResult)
 // 得到 name 相关的分组信息
 // ["{{name}}", "name", index: 7, input: "<div>我是{{name}}</div>", groups: undefined]
```

字符串的**replace()**函数用于在字符串中**用一些字符替换另一些字符**，语法格式如下：

```javascript
var result = '123456'.replace('123', 'abc') // 得到的 result 的值为字符串 'abc456'
```

用while循环替换：

```javascript
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/
var patternResult = null
while(patternResult = pattern.exec(str)) {
   str = str.replace(patternResult[0], patternResult[1])
}
console.log(str) // 输出 <div>name今年age岁了</div>
```

替换为数据中的值：

```javascript
var data = { name: '张三', age: 20 }
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

var patternResult = null
while ((patternResult = pattern.exec(str))) {
   str = str.replace(patternResult[0], data[patternResult[1]])
}
console.log(str)
```



自定义模板引擎，封装template函数：

```javascript
function template(id, data) {
  var str = document.getElementById(id).innerHTML
  var pattern = /{{\s*([a-zA-Z]+)\s*}}/
  var pattResult = null
  while (pattResult = pattern.exec(str)) {
    str = str.replace(pattResult[0], data[pattResult[1]])
  }
  return str
}
```

***

## Ajax加强

### XMLHttpRequest

XMLHttpRequest（简称 xhr）是浏览器提供的 Javascript 对象，通过它，可以请求服务器上的数据资源。之前所学的 jQuery 中的 Ajax 函数，就是基于 xhr 对象封装出来的。

<img src="C:\Users\31330\Pictures\Typora\image-20220807203747106.png" alt="image-20220807203747106" style="zoom:67%;" />

#### 使用xhr发起GET请求

```javascript
// 1. 创建 XHR 对象
var xhr = new XMLHttpRequest()
// 2. 调用 open 函数
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
// 3. 调用 send 函数，发起 Ajax 请求
xhr.send()
// 4. 监听 onreadystatechange 事件
xhr.onreadystatechange = function () {
    //监听 xhr 对象的请求状态 readyState ；与服务器响应的状态 status
  if (xhr.readyState === 4 && xhr.status === 200) {
    // 获取服务器响应的数据
    console.log(xhr.responseText)
  }
}
```

readyState属性：表示当前 Ajax 请求所处的状态，每个 Ajax 请求必然处于以下状态中的一个：

| **值** | **状态**         | **描述**                                            |
| ------ | ---------------- | --------------------------------------------------- |
| 0      | UNSENT           | XMLHttpRequest 对象已被创建，但尚未调用 open方法。  |
| 1      | OPENED           | open() 方法已经被调用。                             |
| 2      | HEADERS_RECEIVED | send() 方法已经被调用，响应头也已经被接收。         |
| 3      | LOADING          | 数据接收中，此时 response 属性中已经包含部分数据。  |
| 4      | DONE             | Ajax 请求完成，这意味着数据传输已经彻底完成或失败。 |

使用 xhr 对象发起带参数的 GET 请求时，只需在调用 xhr.open 期间，为 URL 地址指定参数即可：

这种在 URL 地址后面拼接的参数，叫做·``查询字符串``·。

<img src="C:\Users\31330\Pictures\Typora\image-20220807204403692.png" alt="image-20220807204403692" style="zoom:80%;" />

>
>
>什么是查询字符串?
>
>定义：查询字符串（URL 参数）是指在 URL 的末尾加上用于向服务器发送信息的字符串（变量）。
>格式：将英文的`` ? ``放在URL 的末尾，然后再加上 ``参数＝值`` ，想加上多个参数的话，使用 ``&`` 符号进行分隔。以这个形式，可以将想要发送给服务器的数据添加到 URL 中。
>
>```java
>// 不带参数的 URL 地址
>http://www.liulongbin.top:3006/api/getbooks
>// 带一个参数的 URL 地址
>http://www.liulongbin.top:3006/api/getbooks?id=1
>// 带两个参数的 URL 地址
>http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=西游记
>```
>
>GET请求携带参数的本质:
>
>无论使用 $.ajax()，还是使用 $.get()，又或者直接使用 xhr 对象发起 GET 请求，当需要携带参数的时候，本质上，都是直接将参数以查询字符串的形式，追加到 URL 地址的后面，发送到服务器的。
>
>```javascript
>$.get('url', {name: 'zs', age: 20}, function() {})
>// 等价于
>$.get('url?name=zs&age=20', function() {})
>
>$.ajax({ method: 'GET', url: 'url', data: {name: 'zs', age: 20}, success: function() {} })
>// 等价于
>$.ajax({ method: 'GET', url: 'url?name=zs&age=20', success: function() {} })
>```
>
>什么是URL编码?
>
>URL 地址中，只允许出现英文相关的字母、标点符号、数字，因此，在 URL 地址中不允许出现中文字符。
>如果 URL 中需要包含中文这样的字符，则必须对中文字符进行``编码（转义）``。
>
>浏览器提供了 URL 编码与解码的 API，分别是：
>
>- encodeURI()  编码的函数
>
>- decodeURI()  解码的函数
>
>URL编码的原则：使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符。
>URL编码原则的通俗理解：使用英文字符去表示非英文字符。
>
>![image-20220807210457017](C:\Users\31330\Pictures\Typora\image-20220807210457017.png)

***

#### 使用xhr发起POST请求

```javascript
// 1. 创建 xhr 对象
var xhr = new XMLHttpRequest()
// 2. 调用 open 函数
xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook')
// 3. 设置 Content-Type 属性
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
// 4. 调用 send 函数,同时将数据以查询字符串的形式，提交给服务器
xhr.send('bookname=水浒传&author=施耐庵&publisher=上海图书出版社')
// 5. 监听事件 onreadystatechange
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log(xhr.responseText)
  }
}
```

***

### 数据交换格式

数据交换格式，就是服务器端与客户端之间进行数据传输与交换的格式。
前端领域，经常提及的两种数据交换格式分别是 XML 和 JSON。其中 XML 用的非常少，所以，重点要学习的数据交换格式就是 JSON。

XML 的英文全称是 EXtensible Markup Language，即**可扩展标记语言**。因此，XML 和 HTML 类似，也是一种标记语言。虽然都是标记语言，但是，它们两者之间没有任何的关系。

- HTML 被设计用来描述网页上的内容，是网页内容的载体
- XML 被设计用来传输和存储数据，是数据的载体

JSON 的英文全称是 JavaScript Object Notation，即“JavaScript 对象表示法”。简单来讲，JSON 就是 Javascript 对象和数组的字符串表示法，它使用文本表示一个 JS 对象或数组的信息，因此，JSON 的本质是字符串。
作用：JSON 是一种轻量级的文本数据交换格式，在作用上类似于 XML，专门用于存储和传输数据，但是 JSON 比 XML 更小、更快、更易解析。
现状：JSON 是在 2001 年开始被推广和使用的数据格式，到现今为止，JSON 已经成为了主流的数据交换格式。

JSON 就是用字符串来表示 Javascript 的对象和数组。所以，JSON 中包含对象和数组两种结构，通过这两种结构的相互嵌套，可以表示各种复杂的数据结构。

#### JSON的两种结构

对象结构：对象结构在 JSON 中表示为 { } 括起来的内容。数据结构为 { key: value, key: value, … } 的键值对结构。其中，key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是数字、字符串、布尔值、null、数组、对象6种类型。

```json
{
    name: "zs",
    'age': 20,
    "gender": '男',
    "address": undefined,
    "hobby": ["吃饭", "睡觉", '打豆豆']
    say: function() {}
}
```

数组结构：数组结构在 JSON 中表示为 [ ] 括起来的内容。数据结构为 [ "java", "javascript", 30, true … ] 。数组中数据的类型可以是数字、字符串、布尔值、null、数组、对象6种类型。

```json
[ "java", "python", "php" ]
[ 100, 200, 300.5 ]
[ true, false, null ]
[ { "name": "zs", "age": 20}, { "name": "ls", "age": 30} ]
[ [ "苹果", "榴莲", "椰子" ], [ 4, 50, 5 ] ]
```

>JSON语法注意事项
>
>- 属性名必须使用双引号包裹
>- 字符串类型的值必须使用双引号包裹
>- JSON 中不允许使用单引号表示字符串
>- SON 中不能写注释
>- JSON 的最外层必须是对象或数组格式
>- 不能使用 undefined 或函数作为 JSON 的值
> JSON 的作用：在计算机与网络之间存储和传输数据。
>  JSON 的本质：用字符串来表示 Javascript 对象数据或数组数据

**JSON和JS对象的关系:**

JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。例如：

```javascript
//这是一个对象
var obj = {a: 'Hello', b: 'World'}

//这是一个 JSON 字符串，本质是一个字符串
var json = '{"a": "Hello", "b": "World"}' 

```

**JSON和JS对象的互转:**

1. JSON 字符串转换为 JS 对象，使用 JSON.parse() 方法：

```javascript
var obj = JSON.parse('{"a": "Hello", "b": "World"}')
//结果是 {a: 'Hello', b: 'World'}
```

2.  JS 对象转换为 JSON 字符串，使用 JSON.stringify() 方法：

```javascript
var json = JSON.stringify({a: 'Hello', b: 'World'})
//结果是 '{"a": "Hello", "b": "World"}'
```

**序列化和反序列化**

把数据对象**转换为字符串**的过程，叫做序列化，例如：调用 JSON.stringify() 函数的操作，叫做 JSON 序列化。
把字符串**转换为数据对象**的过程，叫做反序列化，例如：调用 JSON.parse() 函数的操作，叫做 JSON 反序列化。

***

## 封装自己的Ajax函数





略~







***

## XMLHttpRequest Level2的新特性



旧版XMLHttpRequest的缺点:

- 只支持文本数据的传输，无法用来读取和上传文件
- 传送和接收数据时，没有进度信息，只能提示有没有完成

### XMLHttpRequest Level2的新功能

- 可以设置 HTTP 请求的时限
- 可以使用 FormData 对象管理表单数据
- 可以上传文件
- 可以获得数据传输的进度信息

### 设置HTTP请求时限

有时，Ajax 操作很耗时，而且无法预知要花多少时间。如果网速很慢，用户可能要等很久。新版本的 XMLHttpRequest 对象，增加了 timeout 属性，可以设置 HTTP 请求的时限：

```
 xhr.timeout = 3000
```

最长等待时间设为 3000 毫秒。过了这个时限，就自动停止HTTP请求。与之配套的还有一个 timeout 事件，用来指定回调函数：

```javascript
 xhr.ontimeout = function(event){
     alert('请求超时！')
 }
```

### FormData对象管理表单数据

Ajax 操作往往用来提交表单数据。为了方便表单处理，HTML5 新增了一个 FormData 对象，可以模拟表单操作：

```javascript
// 1. 创建 FormData 实例
var fd = new FormData()
// 2. 调用 append 函数，向 FormData 中追加数据
fd.append('uname', 'zs')
fd.append('upwd', '123456')
// 3. 创建 XMLHttpRequest 对象
var xhr = new XMLHttpRequest()
// 4. 指定请求类型与URL地址
xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
// 5. 直接提交 FormData 对象，这与提交网页表单的效果，完全一样
xhr.send(fd)

xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log(JSON.parse(xhr.responseText))
  }
}
```

FormData对象也可以用来获取网页表单的值，示例代码如下：

```javascript
// DOM 操作，获取到 form 表单元素
var form = document.querySelector('#form1')
form.addEventListener('submit', function (e) {
  e.preventDefault()
  // 根据 form 表单创建 FormData 对象，会自动将表单数据填充到 FormData 对象中
  var fd = new FormData(form)
  var xhr = new XMLHttpRequest()
  xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
  xhr.send(fd)

  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
      console.log(JSON.parse(xhr.responseText))
    }
  }
})
```

***

### 上传文件

```html
<!-- 1. 文件选择框 -->
<input type="file" id="file1" />
<!-- 2. 上传文件的按钮 -->
<button id="btnUpload">上传文件</button>
<br />
<!-- 3. img 标签，来显示上传成功以后的图片 -->
<img src="" alt="" id="img" width="800" />
```

```javascript
// 1. 获取到文件上传按钮
var btnUpload = document.querySelector('#btnUpload')
// 2. 为按钮绑定单击事件处理函数
btnUpload.addEventListener('click', function () {
  // 3. 获取到用户选择的文件列表
  var files = document.querySelector('#file1').files
  if (files.length <= 0) return alert('请选择要上传的文件！')
  var fd = new FormData()
  // 将用户选择的文件，添加到 FormData 中
  fd.append('avatar', files[0])
  var xhr = new XMLHttpRequest()
  xhr.open('POST', 'http://www.liulongbin.top:3006/api/upload/avatar')
  xhr.send(fd)

  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
      var data = JSON.parse(xhr.responseText)
      console.log(data);
      if (data.status === 200) {
        // 上传成功
        document.querySelector('#img').src = 'http://www.liulongbin.top:3006' + data.url
      } else {
        // 上传失败
        console.log('图片上传失败！' + data.message)
      }
    }
  }
})
```





**显示文件上传进度**

新版本的 XMLHttpRequest 对象中，可以通过监听 xhr.upload.onprogress 事件，来获取到文件的上传进度。语法格式如下：

```javascript
<!-- bootstrap 中的进度条 -->
<div class="progress" style="width: 500px; margin: 15px 10px;">
  <div class="progress-bar progress-bar-striped active" style="width: 0%" id="percent">
    0%
  </div>
</div>

// 将用户选择的文件，添加到 FormData 中
fd.append('avatar', files[0])
var xhr = new XMLHttpRequest()
// 监听文件上传的进度
xhr.upload.onprogress = function (e) {
  if (e.lengthComputable) {
    // 计算出上传的进度
    var procentComplete = Math.ceil((e.loaded / e.total) * 100)
    console.log(procentComplete)
    // 动态设置进度条
    $('#percent').attr('style', 'width: ' + procentComplete + '%;').html(procentComplete + '%')
  }
}

xhr.upload.onload = function () {
  $('#percent').removeClass().addClass('progress-bar progress-bar-success')
}
```

***

###  jQuery实现文件上传

```html
<input type="file" id="file1" />
<button id="btnUpload">上传文件</button>
<br />
<img src="./images/loading.gif" alt="" style="display: none;" id="loading" />
```

```javascript
$(function () {
  // 监听到Ajax请求被发起了$(document).ajaxStart() 函数会监听当前文档内所有的 Ajax 请求。
  $(document).ajaxStart(function () {
    $('#loading').show()
  })

  // 监听到 Ajax 完成的事件
  $(document).ajaxStop(function () {
    $('#loading').hide()
  })

  $('#btnUpload').on('click', function () {
    //1. 将 jQuery 对象转化为 DOM 对象，并获取选中的文件列表
    var files = $('#file1')[0].files
    if (files.length <= 0) {
      return alert('请选择文件后再上传！')
    }
	// 向 FormData 中追加文件
    var fd = new FormData()
    fd.append('avatar', files[0])

    // 发起 jQuery 的 Ajax 请求，上传文件
    $.ajax({
      method: 'POST',
      url: 'http://www.liulongbin.top:3006/api/upload/avatar',
      data: fd,
      // 不修改 Content-Type 属性，使用 FormData 默认的 Content-Type 值
      contentType: false,
      // 不对 FormData 中的数据进行 url 编码，而是将 FormData 数据原样发送到服务器
      processData: false,
      success: function (res) {
        console.log(res)
      }
    })
  })
})
```

***

## axios

Axios 是专注于**网络数据请求**的库。
相比于原生的 XMLHttpRequest 对象，axios 简单易用。
相比于 jQuery，axios 更加轻量化，只专注于网络数据请求。

### axios发起GET请求

```javascript
document.querySelector('#btn1').addEventListener('click', function () {
  var url = 'http://www.liulongbin.top:3006/api/get'
  // 请求的参数对象
  var paramsObj = { name: 'zs', age: 20 }
  axios.get(url, { params: paramsObj }).then(function (res) {
    console.log(res.data)
  })
})
```

### axios发起POST请求

```javascript
document.querySelector('#btn2').addEventListener('click', function () {
  var url = 'http://www.liulongbin.top:3006/api/post'
  // 要提交到服务器的数据
  var dataObj = { address: '北京', location: '顺义区' }
  axios.post(url, dataObj).then(function (res) {
    // res.data 是服务器返回的数据
    console.log(res.data)
  })
})
```

### 直接使用axios发起请求

axios 也提供了类似于 jQuery 中 $.ajax() 的函数，语法如下：

```javascript
axios({
    method: '请求类型',
    url: '请求的URL地址',
    data: {/*POST数据*/},
    params: {/*GET参数*/}
}).then(callback)
```

1. 直接使用axios发起GET请求:

```javascript
document.querySelector('#btn3').addEventListener('click', function () {
  var url = 'http://www.liulongbin.top:3006/api/get'
  var paramsData = { name: '钢铁侠', age: 35 }
  axios({
    method: 'GET',
    url: url,
    params: paramsData
  }).then(function (res) {
    console.log(res.data)
  })
})
```

2. 直接使用axios发起POST请求:

```javascript
document.querySelector('#btn4').addEventListener('click', function () {
  axios({
    method: 'POST',
    url: 'http://www.liulongbin.top:3006/api/post',
    data: {
      name: 'abc',
      age: 18,
      gender: '女'
    }
  }).then(function (res) {
    console.log(res.data)
  })
})
```

***

## 跨域与JSONP

### 同源策略

同源策略（英文全称 Same origin policy）是浏览器提供的一个安全功能。

如果两个页面的协议，域名和端口都相同，则两个页面具有相同的源。
例如，下表给出了相对于 http://www.test.com/index.html 页面的同源检测：

未指定端口的，端口默认为80.

| **URL**                            | **是否同源** | **原因**                                  |
| ---------------------------------- | ------------ | ----------------------------------------- |
| http://www.test.com/other.html     | 是           | 同源（协议、域名、端口相同）              |
| https://www.test.com/about.html    | 否           | 协议不同（http 与 https）                 |
| http://blog.test.com/movie.html    | 否           | 域名不同（www.test.com 与 blog.test.com） |
| http://www.test.com:7001/home.html | 否           | 端口不同（默认的 80 端口与 7001 端口）    |
| http://www.test.com:80/main.html   | 是           | 同源（协议、域名、端口相同）              |

MDN 官方给定的概念：同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制。

通俗的理解：浏览器规定，A 网站的 JavaScript，不允许和非同源的网站 C 之间，进行资源的交互，例如：

- 无法读取非同源网页的 Cookie、LocalStorage 和 IndexedDB
- 无法接触非同源网页的 DOM
- 无法向非同源地址发送 Ajax 请求

### 跨域

同源指的是两个 URL 的协议、域名、端口一致，反之，则是跨域。
出现跨域的根本原因：浏览器的同源策略不允许非同源的 URL 之间进行资源的交互。
网页：http://www.test.com/index.html
接口：http://www.api.com/userlist

![image-20220808185723157](C:\Users\31330\Pictures\Typora\image-20220808185723157.png)

注意：浏览器允许发起跨域请求，但是，跨域请求回来的数据，会被浏览器拦截，无法被页面获取到！

**实现跨域数据请求:**

两种解决方案: JSONP 和 CORS。
**JSONP**：出现的早，兼容性好（兼容低版本IE）。是前端程序员为了解决跨域问题，被迫想出来的一种临时解决方案。缺点是只支持 GET 请求，不支持 POST 请求。
**CORS**：出现的较晚，它是 W3C 标准，属于跨域 Ajax 请求的根本解决方案。支持 GET 和 POST 请求。缺点是不兼容某些低版本的浏览器。

***

### JSONP

JSONP (JSON with Padding) 是 JSON 的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题。

由于浏览器同源策略的限制，网页中无法通过 Ajax 请求非同源的接口数据。但是 <script> 标签不受浏览器同源策略的影响，可以通过 src 属性，请求非同源的 js 脚本。
因此，JSONP 的实现原理，就是通过 <script> 标签的 src 属性，请求跨域的数据接口，并通过函数调用的形式，接收跨域接口响应回来的数据。

实现：

```javascript
<script>
    function abc(data) {
      console.log('JSONP响应回来的数据是：')
      console.log(data)
    }
</script>

<script src="http://ajax.frontend.itheima.net:3006/api/jsonp?callback=abc&name=ls&age=30"></script>
```

由于 JSONP 是通过 <script> 标签的 src 属性，来实现跨域数据获取的，所以，JSONP 只支持 GET 数据请求，不支持 POST 请求。

注意：JSONP 和 Ajax 之间没有任何关系，不能把 JSONP 请求数据的方式叫做 Ajax，因为 JSONP 没有用到 XMLHttpRequest 这个对象。

### jQuery中的JSONP

jQuery 提供的 $.ajax() 函数，除了可以发起真正的 Ajax 数据请求之外，还能够发起 JSONP 数据请求，例如：

```javascript
$.ajax({
  url: 'http://ajax.frontend.itheima.net:3006/api/jsonp?name=zs&age=20',
  // 代表我们要发起JSONP的数据请求
  // 如果要使用 $.ajax() 发起 JSONP 请求，必须指定 datatype 为 jsonp
  dataType: 'jsonp',
  // 发送到服务端的参数名称，默认值为 callback
  jsonp: 'callback',
  // 自定义的回调函数名称，默认值为 jQueryxxx 格式
  jsonpCallback: 'abc',
  success: function (res) {
    console.log(res)
  }
})
```

jQuery 中的 JSONP，也是通过 <script> 标签的 src 属性实现跨域数据访问的，只不过，jQuery 采用的是动态创建和移除 <script> 标签的方式，来发起 JSONP 数据请求。

- 在发起 JSONP 请求的时候，动态向 <header> 中 append 一个 <script> 标签；
- 在 JSONP 请求成功以后，动态从 <header> 中移除刚才 append 进去的 <script> 标签；



防抖策略（debounce）是当事件被触发后，延迟 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。

<img src="C:\Users\31330\Pictures\Typora\image-20220808211340145.png" alt="image-20220808211340145" style="zoom:80%;" />

防抖的应用场景：

- 用户在输入框中连续输入一串字符时，可以通过防抖策略，只在输入完后，才执行查询的请求，这样可以有效减少请求次数，节约请求资源。

实现输入框的防抖：



```javascript
 var timer = null                    //1. 防抖动的timer
 function debounceSearch(keywords) { //2. 定义防抖的函数
    timer=setTimeout(function(){
    //发起JSONP请求
    getSuggestList(keywords)
    },500)
 }
 $('#ipt').on('keyup', function() {  //3. 在触发 keyup 事件时，立即清空 timer
	clearTimeout(timer)
    // ...省略其他代码
    debounceSearch(keywords)
 })
```

节流：

节流策略（throttle），顾名思义，可以减少一段时间内事件的触发频率。

![image-20220809162336097](C:\Users\31330\Pictures\Typora\image-20220809162336097.png)

节流的应用场景：

- 鼠标连续不断地触发某事件（如点击），只在单位时间内只触发一次；
- 懒加载时要监听计算滚动条的位置，但不必每次滑动都触发，可以降低计算的频率，而不必去浪费 CPU 资源；

使用节流优化鼠标跟随效果：

```javascript
// 1. 获取到图片
var angel = $('#angel')
// 步骤1. 定义节流阀
var timer = null
// 2. 绑定 mousemove 事件
$(document).on('mousemove', function (e) {
  // 3：判断节流阀是否为空，如果不为空，则证明距离上次执行间隔不足16毫秒
  if (timer) { return }
  // 4：开启延时器
  timer = setTimeout(function () {
    $(angel).css('top', e.pageY + 'px').css('left', e.pageX + 'px')
    // 5.当设置了鼠标跟随效果后，清空 timer 节流阀，方便下次开启延时器
    timer = null
  }, 16)
})
```

***

HTTP 协议即超文本传送协议 (HyperText Transfer Protocol) ，它规定了客户端与服务器之间进行网页内容传输时，所必须遵守的传输格式。
例如：
 客户端要以HTTP协议要求的格式把数据提交到服务器
 服务器要以HTTP协议要求的格式把内容响应给客户端

HTTP 协议采用了 **请求/响应** 的交互模型。



客户端发起的请求叫做 HTTP 请求，客户端发送到服务器的消息，叫做 HTTP 请求消息。HTTP 请求消息又叫做 HTTP 请求报文。



![image-20220809164939317](C:\Users\31330\Pictures\Typora\image-20220809164939317.png)

请求头部用来描述客户端的基本信息，从而把客户端相关的信息告知服务器。比如：User-Agent 用来说明当前是什么类型的浏览器；Content-Type 用来描述发送到服务器的数据格式；Accept 用来描述客户端能够接收什么类型的返回内容；Accept-Language 用来描述客户端期望接收哪种人类语言的文本内容。
请求头部由多行 键/值对 组成，每行的键和值之间用英文的冒号分隔。

最后一个请求头字段的后面是一个空行，通知服务器请求头部至此结束。
请求消息中的空行，用来分隔请求头部与请求体。

请求体中存放的，是要通过 POST 方式提交到服务器的数据。只有 POST 请求才有请求体，GET 请求没有请求体！

***

响应消息就是服务器响应给客户端的消息内容，也叫作响应报文。

![image-20220809170704651](C:\Users\31330\Pictures\Typora\image-20220809170704651.png)

状态行由 HTTP 协议版本、状态码和状态码的描述文本 3 个部分组成，他们之间使用空格隔开;

![image-20220809170823806](C:\Users\31330\Pictures\Typora\image-20220809170823806.png)

响应头部用来描述**服务器的基本信息**。响应头部由多行 键/值对 组成，每行的键和值之间用英文的冒号分隔。

https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers

在最后一个响应头部字段结束之后，会紧跟一个空行，用来通知客户端响应头部至此结束。
响应消息中的空行，用来分隔响应头部与响应体。

响应体中存放的，是服务器响应给客户端的资源内容。![image-20220809171001542](C:\Users\31330\Pictures\Typora\image-20220809171001542.png)

***

HTTP的请求方法



| **序号** | **方法** | **描述**                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| 1        | GET      | (查询)发送请求来获得服务器上的资源，请求体中不会包含请求数据，请求数据放在协议头中。 |
| 2        | POST     | (新增)向服务器提交资源（例如提交表单或上传文件）。数据被包含在请求体中提交给服务器。 |
| 3        | PUT      | (修改)向服务器提交资源，并使用提交的新资源，替换掉服务器对应的旧资源。 |
| 4        | DELETE   | (删除)请求服务器删除指定的资源。                             |
| 5        | HEAD     | HEAD 方法请求一个与 GET 请求的响应相同的响应，但没有响应体。 |
| 6        | OPTIONS  | 获取http服务器支持的http请求方法，允许客户端查看服务器的性能，比如ajax跨域时的预检等。 |
| 7        | CONNECT  | 建立一个到由目标资源标识的服务器的隧道。                     |
| 8        | TRACE    | 沿着到目标资源的路径执行一个消息环回测试，主要用于测试或诊断。 |
| 9        | PATCH    | 是对 PUT 方法的补充，用来对已知资源进行局部更新 。           |

![image-20220809171306566](C:\Users\31330\Pictures\Typora\image-20220809171306566.png)

HTTP响应状态码

HTTP 响应状态码（HTTP Status Code），也属于 HTTP 协议的一部分，用来标识响应的状态。
响应状态码会随着响应消息一起被发送至客户端浏览器，浏览器根据服务器返回的响应状态码，就能知道这次 HTTP 请求的结果是成功还是失败了。

HTTP 状态码由三个十进制数字组成，第一个十进制数字定义了状态码的类型，后两个数字用来对状态码进行细分。
HTTP 状态码共分为 5 种类型：

| **分类** | **分类描述**                                                 |
| -------- | ------------------------------------------------------------ |
| 1**      | 信息，服务器收到请求，需要请求者继续执行操作（实际开发中很少遇到 1** 类型的状态码） |
| 2**      | 成功，操作被成功接收并处理                                   |
| 3**      | 重定向，需要进一步的操作以完成请求                           |
| 4**      | 客户端错误，请求包含语法错误或无法完成请求                   |
| 5**      | 服务器错误，服务器在处理请求的过程中发生了错误               |

![image-20220809171412682](C:\Users\31330\Pictures\Typora\image-20220809171412682.png)

完整的 HTTP 响应状态码，可以参考 MDN 官方文档 https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status

2** 范围的状态码，表示服务器已成功接收到请求并进行处理。常见的 2** 类型的状态码如下：

| **状态码** | **状态码英文名称** | **中文描述**                                                |
| ---------- | ------------------ | ----------------------------------------------------------- |
| 200        | OK                 | 请求成功。一般用于 GET 与 POST 请求                         |
| 201        | Created            | 已创建。成功请求并创建了新的资源，通常用于 POST 或 PUT 请求 |

3** 范围的状态码，表示表示服务器要求客户端重定向，需要客户端进一步的操作以完成资源的请求。常见的 3** 类型的状态码如下：

| **状态码** | **状态码英文名称** | **中文描述**                                                 |
| ---------- | ------------------ | ------------------------------------------------------------ |
| 301        | Moved Permanently  | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替 |
| 302        | Found              | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI |
| 304        | Not Modified       | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源（响应消息中不包含响应体）。客户端通常会缓存访问过的资源。 |

4** 范围的状态码，表示客户端的请求有非法内容，从而导致这次请求失败。常见的 4** 类型的状态码如下：

| **状态码** | **状态码英文名称** | **中文描述**                                                 |
| ---------- | ------------------ | ------------------------------------------------------------ |
| 400        | Bad Request        | 1、语义有误，当前请求无法被服务器理解。除非进行修改，否则客户端不应该重复提交这个请求。 2、请求参数有误。 |
| 401        | Unauthorized       | 当前请求需要用户验证。                                       |
| 403        | Forbidden          | 服务器已经理解请求，但是拒绝执行它。                         |
| 404        | Not Found          | 服务器无法根据客户端的请求找到资源（网页）。                 |
| 408        | Request Timeout    | 请求超时。服务器等待客户端发送的请求时间过长，超时。         |

5** 范围的状态码，表示服务器未能正常处理客户端的请求而出现意外错误。常见的 5** 类型的状态码如下：

| **状态码** | **状态码英文名称**    | **中文描述**                                                 |
| ---------- | --------------------- | ------------------------------------------------------------ |
| 500        | Internal Server Error | 服务器内部错误，无法完成请求。                               |
| 501        | Not Implemented       | 服务器不支持该请求方法，无法完成请求。只有 GET 和 HEAD 请求方法是要求每个服务器必须支持的，其它请求方法在不支持的服务器上会返回501 |
| 503        | Service Unavailable   | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。       |



***

验证手机号的正则:const regex = /^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/;
