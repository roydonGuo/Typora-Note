
## axios

> axios 是一个专注于网络请求的库！

axios 的基本使用（前提npm了axios或者导入了axios的js文件）：

1. 发起 GET 请求：

   ```js
   axios({
     // 请求方式
     method: 'GET',
     // 请求的地址
     url: 'http://www.example.xyz/xxx',
     // URL 中的查询参数
     params: {
       id: 1
     }
   }).then(function (result) {
     console.log(result)
   })
   ```

2. 发起 POST 请求：

   ```js
   document.querySelector('#btnPost').addEventListener('click', async function () {
     // 如果调用某个方法的返回值是 Promise 实例，则前面可以添加 await！
     // await 只能用在被 async “修饰”的方法中
     const { data: res } = await axios({
       method: 'POST', 
       url: 'http://www.example.xyz/xxx',
       data: {
         name: 'zs',
         age: 20
       }
     })
     console.log(res)
   })
   ```

# Vue 2

vue2加速链接

> <!-- 开发环境版本，包含了有帮助的命令行警告 -->
>
> ```html
> <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
> ```

> <!--  vue3官网：-->
>
> [https://cn.vuejs.org](https://cn.vuejs.org/guide/quick-start.html#try-vue-online)
>
> <!--  vue2官网：-->
>
> [https://v2.cn.vuejs.org/](https://v2.cn.vuejs.org/)

---

## 什么是 vue

1. 构建用户界面
   + 用 vue 往 html 页面中填充数据，非常的方便
2. 框架
   + 框架是一套现成的解决方案，程序员只能遵守框架的规范，去编写自己的业务功能！
   + 要学习 vue，就是在学习 vue 框架中规定的用法！
   + vue 的指令、组件（是对 UI 结构的复用）、路由、Vuex、vue 组件库
   + 只有把上面老师罗列的内容掌握以后，才有开发 vue 项目的能力！

---

## vue 的两个特性

1. ==**数据驱动视图**==：

   + vue 会监听数据的变化，数据的变化会驱动视图自动更新，单向。
   + 好处：程序员只管把数据维护好，那么页面结构会被 vue 自动渲染出来！

2. ==**双向数据绑定**==：

   - 在网页中，form 表单负责**采集数据**，Ajax 负责**提交数据**。

   + js 数据的变化，会被自动渲染到页面上。
   + 页面上表单采集的数据发生变化的时候，会被 vue 自动获取到，并更新到 js 数据中。

> 注意：数据驱动视图和双向数据绑定的底层原理是 **MVVM**（Mode 数据源、View 视图、ViewModel 就是 vue 的实例）

![image-20221011112604101](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111747164.png)

MVVM 指的是 Model、View 和 ViewModel，它把每个 HTML 页面都拆分成了这三个部分(上图)。在 MVVM 概念中：

- Model 表示当前页面渲染时所依赖的数据源。
- View 表示当前页面所渲染的 DOM 结构。
- ViewModel 表示 vue 的实例，它是 MVVM 的核心。



***

## Vue2模板

![image-20221011112837910](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111749007.png)

```vue
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Vue2</title>
</head>
<body>
  <div id="app">
    {{ msg }}
  </div>
  <!-- 引入 vue.js -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var app = new Vue({
      // vue挂载的位置，id为app的一个div上
      el: "#app",
      // vue要渲染的数据
      data:{
        msg: "hello vue"
      }
    })
  </script>
</body>
</html>
```

***

## Vue 调试工具



安装 vue-devtools 调试工具：

vue 官方提供的 vue-devtools 调试工具，能够方便开发者对 vue 项目进行调试与开发。

- Chrome 浏览器在线安装 vue-devtools ，使用此网址直接搜vue-devtools：[https://chrome.zzzmh.cn/index#/index](https://chrome.zzzmh.cn/index#/index)
- FireFox 浏览器在线安装 vue-devtools ：https://addons.mozilla.org/zh-CN/firefox/addon/vue-js-devtools/

插件下载好的安装具体说明在文档中包含。安装好后重启浏览器即可。

之后打开调试面板即可看到 Vue 面板。

![image-20221011113509059](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111749310.png)

![image-20221011113756345](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111749097.png)

***

## vue指令

==指令（Directives）==是 vue 为开发者提供的模板语法，用于辅助开发者渲染页面的基本结构。

指令具体按照用途可以分为如下六大类：

* ① 内容渲染指令

* ② 属性绑定指令

* ③ 事件绑定指令

* ④ 双向绑定指令

* ⑤ 条件渲染指令

* ⑥ 列表渲染指令

> 注意：指令是 vue 开发中最基础、最常用、最简单的知识点。

### 内容渲染

- ``{{ }}`` 插值表达式：在实际开发中用的最多，只是内容的占位符，不会覆盖原有的内容！例如上图模板``{{ msg }}``。

- ``v-text``：把数据按文本输出

- ``v-html``：若数据文本带有h5标签，则会渲染输出。相当于设置元素的 innerHTML

例如：	

```vue
v-text="<a href='https://roydon.xyz'>roydon</a>";
<!-- 输出<a href='https://roydon.xyz'>roydon</a> -->

v-html="<a href='https://roydon.xyz'>roydon</a>";
<!-- 输出roydon超链接 -->
```

![image-20221005224113543](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111749142.png)



### 属性绑定

- ``v-bind:`` 指令，为**元素的属性**动态绑定值。简写为英文的 `:`

> 注意：v-bind 是为元素的属性attitude动态绑定值，例如class，src，id，type...

```vue
<div v-bind:class="divClass">div内容区域</div>
<h1 :class="myh1">h1标题</h1> 
<!-- v-bind 简写为: -->
<div :class="divClass">div内容区域</div>
<!--  如果绑定内容需要进行动态拼接，则字符串的外面应该包裹单引号  -->
<div :class="'divClass' + index">这是一个 div</div>
```

![image-20221006101956334](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111750190.png)



### 事件绑定

- ``v-on``，简写为`@`

主要是为**元素绑定事件**，事件名称自定义，`methods`里写对应方法即可。

```vue
<div id="app">
    <input type="button" value="点击触发" v-on:click="方法名">
    <input type="button" value="双击触发" v-on:dblclick="方法名">
    <input type="button" value="点击触发" @click="方法名">
    <input type="text" value="回车触发事件" @keyup.enter="方法名">
</div>
```

![image-20221006101424396](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111750877.png)

- `$event` 是 vue 提供的特殊变量，用来表示原生的事件参数对象 event。$event 可以解决事件参数对象 event 被覆盖的问题。

如果是html原生元素，`$event`代表获取元素的 DOM 对象；

如果是自定义组件，如饿了么ui，vant组件的非html元素，`$event`获取的是组件当前的值，此时的$event相当于参数。

```vue
<div id="app">
    <input type="button" :value="count" @click="add(10,$event)" />
</div>
<!-- vue -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el: "#app",
        data: {
            count: 0
        },
        methods: {
            add(num, e) {
                this.count += num
                console.log(e)//打印的是对应的元素dom对象
            }
        },
    })
</script>
```



- 事件修饰符



在事件处理函数中调用 event.preventDefault() 或 event.stopPropagation() 是非常常见的需求。

因此，vue 提供了**事件修饰符**的概念，来辅助程序员更方便的**对事件的触发进行控制**。



> + `.prevent`
>
>   ```xml
>   <a @click.prevent="xxx">链接</a>
>   ```
>
> + `.stop`
>
>   ```xml
>   <button @click.stop="xxx">按钮</button>
>   ```
>   
>   等......
>

常用的 5 个事件修饰符如下：

![image-20221011160314501](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111750191.png)

- 按键修饰符

在监听键盘事件时，我们经常需要判断详细的按键。此时，可以为键盘相关的事件添加按键修饰符，例如：

```vue
<div id="app">
  {{ msg }}<br>
  <input @keyup.enter="submit" /><br>
  <input @keyup.esc="clear" />
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: "#app",
    data: {
      msg: "hello vue2",
    },
    methods: {
      submit() {
        alert("点击了enter回车键")
      },
      clear() {
        alert("点击了esc退出键")
      }
    },
  })
</script>
```



### 条件渲染

条件渲染指令用来辅助开发者按需**控制 DOM 的显示与隐藏**。条件渲染指令有如下两个:

- `v-show`：原理是 **display 设为 none**
- `v-if`：原理是**动态地创建或移除 DOM 元素**

⚫ 如果需要非常频繁地切换，则使用 v-show 较好

⚫ 如果在运行时条件很少改变，则使用 v-if 较好

> 在实际开发中，绝大多数情况，不用考虑性能问题，直接使用 v-if 就好了！！！

- `v-else`

v-if 可以单独使用，或配合 v-else 指令一起使用：

```vue
<div id="app">
  <h1 v-if="number>=60">成绩合格</h1>
  <h1 v-else>成绩不及格</h1>
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: "#app",
    data: {
      number: 90
    }
  })
</script>
```

- `v-else-if `

```vue
<div id="app">
  <h1 v-if="number>=80">成绩优秀！</h1>
  <h1 v-else-if="number>=60&number<80">成绩合格</h1>
  <h1 v-else>成绩不及格</h1>
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: "#app",
    data: {
      number: 90
    }
  })
</script>
```



> 注意：v-else 和 v-else-if 指令都必须配合 v-if 指令一起使用，否则将不会被识别！

### 双向绑定

- `v-model `双向数据绑定，用于表单当中。

表单数据的变化会动态改变data中数据的值。

data中数据值的变化动态渲染到绑定v-model的元素中。

为了方便对用户输入的内容进行处理，vue 为 v-model 指令提供了 3 个修饰符，分别是：

![image-20221011161906840](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111750065.png)

```vue
<div id="app">
    <input type="text" v-model="content" />
    <h1>{{content}}</h1>
</div>
<!-- vue -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el: "#app",
        data: {
            content: ''
        },
        methods: {
        },
    })
</script>
```



### 列表渲染

- `v-for`

vue 提供的列表渲染指令，用来辅助开发者基于一个**数组**来**循环渲染一个列表结构**，语法格式：

```vue
<!-- item就是循环数组的每一项； person 就是待循环的数组 -->
<h1 v-for="item in person">
    姓名：{{ item.name }}
</h1>
<!-- 同时还可以遍历出每一项的索引值(可选参数) -->
<h1 v-for="(item,index) in person">
    姓名：{{ item.name }}
    索引：{{ index }}
</h1>
<!-- v-for 指令中的item和index都是形参，可任意指定符合规范的名字 -->
//////////////////////////
data: {
  person: [
	{id: 1,name: 'roydon'},	
    {id: 2,name: 'yicheng'}
  ]
}
```

如下：

>  ==注意==：遍历时必须要绑定一个 key，推荐使用 id，key 值类型为数字或者字符串（number/string）。
>
> 注意 key 值重复会报错：Duplicate keys detected。
>
> 索引 index 不具有唯一性，不推荐当作 key。

```vue
<div id="app">
    <!-- <div v-for="item in imgSrc" :key="item.id">
        <img alt="" :src="item.urll" />
    </div> -->
    <!-- index：元素索引 -->
    <img alt="" v-for="(item,index) in imgSrc" :key="item.id" :src="item.urll" />
</div>
<!-- vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el: "#app",
        data: {
            imgSrc: [
                { id: 1, urll: "https://img1.imgtp.com/2022/10/02/x2zOdyMi.png" },
                { id: 2, urll: "https://img1.imgtp.com/2022/10/02/6OcEDlzP.png" },
                { id: 3, urll: "https://img1.imgtp.com/2022/10/02/PCii39ly.png" },
            ],
        }
    })
</script>
```

---

> 案例：品牌列表 P56

***

## 过滤器*

**过滤器（Filters）**是 vue 为开发者提供的功能，常用于文本的格式化。

过滤器可以用在两个地方：插值表达式和 v-bind 属性绑定。

不过，在 Vue3 中剔除了过滤器，所以也不必掌握。

过滤器应该被添加在 JavaScript 表达式的**尾部**，由`管道符'|'`进行调用，示例代码如下

```vue
<div id="app">
  <!-- 在双花括号中通过管道符调用 capitalize 过滤器，对 msg 的值进行格式化 -->
  <h1>{{ msg | capitalize }}</h1>
  <!-- 在 v-bind 中通过管道符调用 formatId 过滤器，对 rawId 的值进行格式化 -->
  <div v-bind:id="rawId | formatId"></div>
</div>
```

### 定义过滤器

创建Vue示例后，可以在 `filters 节点`中定义·过滤器，示例代码如下：

```vue
<div id="app">
  <h1>{{msg | capitalize}}</h1>
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: "#app",
    data: {
      msg: "hello",
    },
    filters: {
      capitalize(msg) {
        // 首字母转大写
        return msg.charAt(0).toUpperCase() + msg.slice(1)
      }
    }
  })
</script>
```

### 私有过滤器

在 filters 节点下定义的过滤器称为**私有过滤器**，因为它只能在此Vue实例挂载的元素中使用。

### 全局过滤器

定义一个全局可用的过滤器：Vue.filter()

```vue
<div id="app">
  <h1>{{msg | capitalize}}</h1>
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  // 定义全局可用过滤器
  Vue.filter('capitalize', (msg) => {
    return msg.toUpperCase()
  })
  var app = new Vue({
    el: "#app",
    data: {
      msg: "hello",
    }
  })
</script>
```

连续调用多个全局过滤器：

```javascript
{{msg | filterA | filterB}}
<!-- msg 先由 filterA 处理，处理之后的值交由 filterB 处理 -->
```

### 过滤器传参

**过滤器的本质就是 JavaScript 函数**，因此可以接收参数，例如：

```vue
<h1>{{msg | filterA(arg1,arg2)}}</h1>
// 第一个参数永远是管道符之前待处理的值
Vue.filter('filterA', (msg,arg1,arg2) => {
  // 代码逻辑
})
```

例如下方案例：控制字符长度

```vue
<div id="app">
  <h1>{{msg | capitalize | maxLength(5)}}</h1>
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  Vue.filter('capitalize', (msg) => {
    return msg.toUpperCase()
  })
  Vue.filter('maxLength', (str, len = 20) => {
    console.log(len);// 无论形参赋何值，len只等于过滤器传进来的值。所以此处打印 5
    if (str.length <= len) return str
    return str.slice(0, len) + '...'
  })
  var app = new Vue({
    el: "#app",
    data: {
      msg: "hello vue2.js",
    }
  })
</script>
```



***

## watch 侦听器

watch 侦听器允许开发者**监视数据的变化**，从而**针对数据的变化做特定的操作**。语法格式如下：

```vue
<div id="app">
  <h1>{{msg}}</h1>
  <input v-model:value="msg" style="border: none;">
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: "#app",
    data: {
      msg: "hello vue2.js",
    },
    watch: {
      msg(newVal, oldVal) {
        console.log(newVal + '|' + oldVal);
      }
    }
  })
</script>
```

![image-20221011181237152](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111813237.png)



### immediate 选项

默认情况下，组件在初次加载完毕后不会调用watch 侦听器。如果想让watch 侦听器立即被调用，则需要使用immediate 选项。示例代码如下：

```vue
<div id="app">
  <h1>{{msg}}</h1>
  <input v-model:value="msg" style="border: none;">
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: "#app",
    data: {
      msg: "hello vue2.js",
    },
    watch: {
      msg: {
        // handler 是固定写法，表示当 msg 的值变化时，自动调用 handler 处理函数
        handler: async function (newVal) {
          if (newVal === '') return
          // 判断值是否合法的 axios，前提是先导入axios模块，这里就不演示了
          const { data: res } = await axios.get('https://www.escook.cn/api/finduser/' + newVal)
          console.log(res)
        },
        // 表示页面初次渲染好之后，就立即触发当前的 watch 侦听器
        immediate: true
      }
    }
  })
</script>
```

### deep 选项

如果 **watch 侦听的是一个对象**，如果对象中的属性值发生了变化，则无法被监听到。此时需要使用 deep 选项

```vue
<div id="app">
  <h1>{{userInfo}}</h1>
  <input v-model:value="userInfo.name">
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: "#app",
    data: {
      userInfo: {
        name: 'roydon',
        age: 18
      }
    },
    watch: {
      userInfo: {
        handler(newVal) {
          console.log(newVal.name);
        },
        deep: true
      }
    }
  })
</script>
```

![image-20221011182938840](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111830980.png)

### 监听对象单个属性

```json
watch: {
  'userInfo.age': {
    handler(newVal) {
      console.log(newVal);
    },
    deep: true
  }
}
```

so：

1. 方法格式的侦听器
   + 缺点1：无法在刚进入页面的时候，自动触发！！！
   + 缺点2：如果侦听的是一个对象，如果对象中的属性发生了变化，不会触发侦听器！！！
2. 对象格式的侦听器
   + 好处1：可以通过 **immediate** 选项，让侦听器自动触发！！！
   + 好处2：可以通过 **deep** 选项，让侦听器深度监听对象中每个属性的变化！！！

***

## 计算属性

计算属性指的是通过`一系列运算`之后，最终得到一个`属性值`。这个动态计算出来的属性值可以被模板结构或methods 方法使用

```vue
<div id="app">
  <h1>{{ rgb }}</h1>
  <input type="button" value="获取rgb" @click="show">
</div>
<!-- 引入 vue.js -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: "#app",
    data: {
      r: 10, g: 20, b: 30
    },
    computed:{
      rgb(){
        return `rgb(${this.r+10},${this.g-10},${this.b*1})`
      }
    },
    methods: {
      show(){
        // 注意此处不加括号
        console.log(this.rgb);
      }
    },
  })
</script>
```

> ==注意==：虽然**声明的时候被定义为方法**，但是计算属性的**本质是一个属性**
>
> 计算属性会**缓存计算的结果**，只有计算属性**依赖的数据变化时才会重新运算**

***

## 单页面应用

单页面应用程序（英文名：Single Page Application）简称SPA。

只有一个 html 页面。记住 Vue 就是单页面即可，就是往一个页面塞组件。因为 Vue 的观念就是组件化：

后续讲解 Vue-cli 创建出一个完整的 Vue2 项目如下图就可以直观的看到：

![image-20221011184808371](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111848000.png)



***

## vue-cli

vue-cli 是Vue.js 开发的标准工具。它简化了程序员基于webpack 创建工程化的Vue 项目的过程。

官网：https://cli.vuejs.org/zh/

安装：

```shell
npm install -g @vue/cli
# 或者
yarn global add @vue/cli
```

创建一个项目（名字为 my-project）：

```shell
vue create my-project
# 或者
vue ui
```

具体创建步骤前往：[https://blog.csdn.net/m0_51390535/article/details/126966696](https://blog.csdn.net/m0_51390535/article/details/126966696?spm=1001.2014.3001.5502)

如果命令行界面创建时进度条不动了，可以：

```vue
ctrl + d
```

vue 项目中 src 目录的构成：

```shell
assets 文件夹：存放项目中用到的静态资源文件，例如：css 样式表、图片资源
components 文件夹：程序员封装的、可复用的组件，都要放到 components 目录下
main.js 是项目的入口文件。整个项目的运行，要先执行 main.js
App.vue 是项目的根组件。
```



***

## Vue 项目运行流程

在工程化的项目中，vue 要做的事情很单纯：通过main.js 把App.vue 渲染到index.html 的指定区域中。

其中：

① App.vue 用来编写待渲染的模板结构

② index.html 中需要预留一个el 区域

③ main.js 把App.vue 渲染到了index.html 所预留的区域中

***

## Vue 组件

组件化开发指的是：根据封装的思想，把页面上可重用的UI 结构封装为组件，从而方便项目的开发和维护。

组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、独立和通常可复用的组件构建大型应用。仔细想想，几乎任意类型的应用界面都可以抽象为一个组件树：

![Component Tree](https://v2.cn.vuejs.org/images/components.png)

每个.vue 组件都由3 部分构成，分别是：

![image-20221011185937911](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210111859751.png)

- template -> 组件的**模板结构**，它不会被渲染成dom，只能包含唯一的根节点

- script -> 组件的**JavaScript 行为**，export中的 data 必须是一个函数。
- style -> 组件的**样式css**，每个组件单独设置样式需在 style 标签内指定 scoped 属性

> 其中，每个组件中必须包含template 模板结构，而script 行为和style 样式是可选的组成部分。

***

### 使用组件

#### 注册私有组件

例如在 App.vue 中使用 vue-cli 创建项目时生成的 HelloWorld.vue 组件。

步骤一：import 导入组件

```js
import HelloWorld from "./components/HelloWorld.vue";
```

步骤二：使用 components 节点注册组件

```javascript
export default {
  name: "App",
  components: {
	// 名称就是导入时定义的名称
    HelloWorld,
  },
};
```

步骤三：以标签的形式使用组件

```vue
<div id="app">
  <HelloWorld msg="Welcome to Your Vue.js App" />
</div>
```

#### 注册全局组件

在vue 项目的 `main.js 入口文件`中，通过`Vue.component()`方法，可以注册全局组件。

```js
import Vue from 'vue'
import App from './App.vue'

// 导入全局组件
import HelloWorld from '@/components/HelloWorld.vue'
Vue.component('MyHelloWorld',HelloWorld)

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).$mount('#app')
```

***

### props

是组件的自定义属性，当父组件向子组件传值时，只需要在子组件定义一个props，并且父组件给这个props属性指定值即可实现父子传值。



![image-20221011204959752](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210112050455.png)

![image-20221011205150164](https://raw.githubusercontent.com/roydonGuo/Typora-Pic/main/md-pic202210112051839.png)

> 当组件被复用，每个组件会独立维护自己的 props，因为每使用一次组件，就会有一个它的新的`实例`被创建。
>
> 为了防止组件互相污染，`data`必须是一个函数。*（不必深究）

props是只读的，若需要修改，可以间接借助data，自定义一个数据把props的数据传进来即可。

props在自定义属性时，也可以指定参数：

```js
export default {
  props: {
    msg: {
      // 必填项
      required: true
      // 声明类型
      type: String,// Number、Object、...
      // 默认值
      default: "",
    },
  },
};
```



### 组件传值

#### 父向子传值

使用`自定义属性props`：

![image-20220820205251370](C:\Users\31330\Pictures\Typora\image-20220820205251370.png)

#### 子向父传值

使用`自定义事件$emit`：

![image-20220820205355516](C:\Users\31330\Pictures\Typora\image-20220820205355516.png)

当子组件通过`$emit()`传入的第二个参数为具体的数值，例如：

```js
v-on:click="$emit('numchange',10)"
```

这个时候父组件可以通过`$event` 访问到被抛出的这个值。

![image-20221012112008219](C:\Users\31330\Pictures\Typora\image-20221012112008219.png)

![image-20221012114152120](C:\Users\31330\Pictures\Typora\image-20221012114152120.png)

#### 兄弟组件之间数据共享

使用`eventBus`，使用步骤：

1. 创建 `eventBus.js` 模块，并向外共享一个 Vue 的实例对象

2. 在**数据发送方**，调用 `bus.$emit('事件名称', 要发送的数据)` 方法触发自定义事件

3. 在**数据接收方**，调用 `bus.$on('事件名称', 事件处理函数)` 方法注册一个自定义事件

![image-20220820205948870](C:\Users\31330\Pictures\Typora\image-20220820205948870.png)

***

### 组件生命周期

`生命周期（Life Cycle）`是指一个组件从`创建`->` 运行`-> `销毁`的整个阶段，强调的是一个时间段。

`生命周期函数`：是由vue 框架提供的内置函数，会伴随着组件的生命周期，自动按次序执行。

> 注意：生命周期强调的是时间段，生命周期函数强调的是时间点。

下方是 Vue 生命周期图示(来源于官方)

![vue2生命周期](https://v2.cn.vuejs.org/images/lifecycle.png)







![img](https://upload-images.jianshu.io/upload_images/11370083-f279314aef6741db.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/1080/format/webp)







## 插槽

![image-20221020210244720](C:\Users\31330\Pictures\Typora\image-20221020210244720.png)



传值问题：

![image-20221020212107622](C:\Users\31330\Pictures\Typora\image-20221020212107622.png)

动态绑定数据：

![image-20221020212435685](C:\Users\31330\Pictures\Typora\image-20221020212435685.png)

接收形式：

![image-20221020212508869](C:\Users\31330\Pictures\Typora\image-20221020212508869.png)

另一种接收数据的形式：

![image-20221020212805955](C:\Users\31330\Pictures\Typora\image-20221020212805955.png)







[Vue2.0-04.路由的基本用法 - 安装和配置路由_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1zq4y1p7ga/?p=178&spm_id_from=pageDriver&vd_source=616a9dd528080cf576646147166fe033)





## axios

![image-20221021140915027](C:\Users\31330\Pictures\Typora\image-20221021140915027.png)











## 路由



![image-20221021165956434](C:\Users\31330\Pictures\Typora\image-20221021165956434.png)
