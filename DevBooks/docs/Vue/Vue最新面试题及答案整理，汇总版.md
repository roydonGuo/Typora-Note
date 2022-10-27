# Vue最新面试题及答案整理，汇总版


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、Vue2.x组件通信有哪些方式？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#1vue2x组件通信有哪些方式)  


**父子组件通信**

父->子`props`，子->父 `$on、$emit`

获取父子组件实例 `$parent、$children`

`Ref` 获取实例的方式调用组件的属性或者方法

`Provide、inject` 官方不推荐使用，但是写组件库时很常用

**兄弟组件通信**

`Event Bus` 实现跨组件通信 `Vue.prototype.$bus = new Vue`

`Vuex`

**跨级组件通信**

`Vuex`

`$attrs、$listeners`

`Provide、inject`


### [2、聊聊你对Vue.js的template编译的理解？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#2聊聊你对vuejs的template编译的理解)  


简而言之，就是先转化成AST树，再得到的render函数返回VNode（Vue的虚拟DOM节点）

**详情步骤：**

**1、** 首先，通过compile编译器把template编译成AST语法树（abstract syntax tree 即 源代码的抽象语法结构的树状表现形式），compile是createCompiler的返回值，createCompiler是用以创建编译器的。另外compile还负责合并option。

**2、** 然后，AST会经过generate（将AST语法树转化成render funtion字符串的过程）得到render函数，render的返回值是VNode，VNode是Vue的虚拟DOM节点，里面有（标签名、子节点、文本等等）


### [3、data为什么是一个函数？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#3data为什么是一个函数)  


这是有JavaScript的特性所导致，在component中，data必须以函数的形式存在，不可以是对象。

组建中的data写成一个函数，数据以函数返回值的形式定义，这样每次复用组件的时候，都会返回一份新的data，相当于每个组件实例都有自己私有的数据空间，它们只负责各自维护的数据，不会造成混乱。而单纯的写成对象形式，就是所有的组件实例共用了一个data，这样改一个全都改了。


### [4、vue中的v-cloak的理解？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#4vue中的v-cloak的理解)  


使用 v-cloak 指令设置样式，这些样式会在 Vue 实例编译结束时，从绑定的 HTML 元素上被移除。

一般用于解决网页闪屏的问题，在对一个的标签中使用v-cloak，然后在样式中设置[v-cloak]样式,[v-cloak]需写在 link 引入的css中，或者写一个内联css样式，写在import引入的css中不起作用。


### [5、Vue事件绑定原理说一下](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#5vue事件绑定原理说一下)  


原生事件绑定是通过`addEventListener`绑定给真实元素的，组件事件绑定是通过Vue自定义的`$on`实现的。


### [6、v-if和v-for的优先级](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#6v-if和v-for的优先级)  


当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级，这意味着 v-if 将分别重复运行于每个 v-for 循环中。所以，不推荐v-if和v-for同时使用。

如果v-if和v-for一起用的话，vue中的的会自动提示v-if应该放到外层去。


### [7、scss是什么？在vue.cli中的安装使用步骤是？有哪几大特性？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#7scss是什么在vuecli中的安装使用步骤是有哪几大特性)  


css的预编译。

**使用步骤：**

**1、** 第一步：用npm 下三个loader（sass-loader、css-loader、node-sass）

**2、** 第二步：在build目录找到webpack.base.config.js，在那个extends属性中加一个拓展.scss

**3、** 第三步：还是在同一个文件，配置一个module属性

**4、** 第四步：然后在组件的style标签加上lang属性 ，例如：lang=”scss”

**有哪几大特性:**

**1、** 可以用变量，例如（$变量名称=值）；

**2、** 可以用混合器，例如（）

**3、** 可以嵌套


### [8、如何获取dom?](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#8如何获取dom)  


ref="domName" 用法：this.$refs.domName


### [9、JS中的宿主对象与原生对象有何不同？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#9js中的宿主对象与原生对象有何不同)  


宿主对象:这些是运行环境提供的对象。这意味着它们在不同的环境下是不同的。例如，浏览器包含像windows这样的对象，但是Node.js环境提供像Node List这样的对象。

原生对象:这些是JS中的内置对象。它们也被称为全局对象，因为如果使用JS，内置对象不受是运行环境影响。


### [10、RouterLink在IE和Firefox中不起作用（路由不跳转）的问题](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案整理，汇总版.md#10routerlink在ie和firefox中不起作用路由不跳转的问题)  


方法一：只用a标签，不适用button标签；方法二：使用button标签和Router.navigate方法


### 11、怎么定义 vue-router 的动态路由? 怎么获取传过来的值？
### 12、请说下封装 vue 组件的过程？
### 13、如何封装一个vue组件？
### 14、$nextTick的使用？
### 15、v-model的理解？
### 16、vue.cli中怎样使用自定义的组件？有遇到过哪些问题吗？
### 17、你如何捕获元素上的点击事件？
### 18、第一次页面加载会触发哪几个钩子？
### 19、vue生命周期的作用是什么？
### 20、你们vue项目是打包了一个js文件，一个css文件，还是有多个文件？
### 21、你都做过哪些Vue的性能优化，编码阶段
### 22、v-show 指令的用途是什么？
### 23、解释 JS 中的函数提升
### 24、v-for中的key的理解？
### 25、说一下v-model的原理
### 26、解释 JS 事件委托模型？
### 27、解释JS中的MUL函数





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




