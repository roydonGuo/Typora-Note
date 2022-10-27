# Vue最新面试题及答案附答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、vue常用的修饰符？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#1vue常用的修饰符)  


**1、** .stop：等同于JavaScript中的event.stopPropagation()，防止事件冒泡；

**2、** .prevent：等同于JavaScript中的event.preventDefault()，防止执行预设的行为（如果事件可取消，则取消该事件，而不停止事件的进一步传播）；

**3、** .capture：与事件冒泡的方向相反，事件捕获由外到内；

**4、** .self：只会触发自己范围内的事件，不包含子元素；

**5、** .once：只会触发一次。


### [2、vue常用的修饰符](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#2vue常用的修饰符)  


**1、** .stop：等同于JavaScript中的event.stopPropagation()，防止事件冒泡；

**2、** .prevent：等同于JavaScript中的event.preventDefault()，防止执行预设的行为（如果事件可取消，则取消该事件，而不停止事件的进一步传播）；

**3、** .capture：与事件冒泡的方向相反，事件捕获由外到内；

**4、** .self：只会触发自己范围内的事件，不包含子元素；

**5、** .once：只会触发一次。


### [3、Vue-router跳转和location.href有什么区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#3vue-router跳转和locationhref有什么区别)  


**1、** 使用location.href='/url'来跳转，简单方便，但是刷新了页面；

**2、** 使用history.pushState('/url')，无刷新页面，静态跳转；

**3、** 引进router，然后使用router.push('/url')来跳转，使用了diff算法，实现了按需加载，减少了dom的消耗。

**4、** 其实使用router跳转和使用history.pushState()没什么差别的，因为vue-router就是用了history.pushState()，尤其是在history模式下。


### [4、简单说一下Vue2.x响应式数据原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#4简单说一下vue2x响应式数据原理)  


Vue在初始化数据时，会使用`Object.defineProperty`重新定义data中的所有属性，当页面使用对应属性时，首先会进行依赖收集(收集当前组件的`watcher`)如果属性发生变化会通知相关依赖进行更新操作(`发布订阅`)。


### [5、vuex有哪几种属性？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#5vuex有哪几种属性)  


有五种，分别是 State、 Getter、Mutation 、Action、 Module

**1、** state => 基本数据(数据源存放地)

**2、** getters => 从基本数据派生出来的数据

**3、** mutations => 提交更改数据的方法，同步！

**4、** actions => 像一个装饰器，包裹mutations，使之可以异步。

**5、** modules => 模块化Vuex


### [6、路由跳转和location.href的区别？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#6路由跳转和locationhref的区别)  


使用location.href='/url'来跳转，简单方便，但是刷新了页面；

使用路由方式跳转，无刷新页面，静态跳转；


### [7、销毁过程](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#7销毁过程)  


`父beforeDestroy->子beforeDestroy->子destroyed->父destroyed`


### [8、什么是vue生命周期？](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#8什么是vue生命周期)  


Vue 实例从创建到销毁的过程，就是生命周期。也就是从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程，我们称这是 Vue 的生命周期。


### [9、用纯JS编写一个程序来反转字符串](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#9用纯js编写一个程序来反转字符串)  


使用内置函数：内置函数reverse()直接反转字符串。

```
str="jQuery";
str = str.split("")
str = str.reverse()
str = str.join("")
alert(str);
```

首先将字符串拆分为数组，然后反转数组，最近将字符连接起来形成字符串。 使用循环:首先，计算字符串中的字符数，然后对原始字符串应用递减循环，该循环从最后一个字符开始，打印每个字符，直到count变为零。


### [10、分别简述computed和watch的使用场景](https://gitee.com/souyunku/DevBooks/blob/master/docs/Vue/Vue最新面试题及答案附答案汇总.md#10分别简述computed和watch的使用场景)  


**computed:**

当一个属性受多个属性影响的时候就需要用到computed

最典型的栗子： 购物车商品结算的时候

**watch:**

当一条数据影响多条数据的时候就需要用watch

栗子：搜索数据


### 11、数组去重复的方法有哪些
### 12、cancas和SVG的是什么以及区别
### 13、解释一下 "use strict" ? “
### 14、vue更新数组时触发视图更新的方法
### 15、JS中的Array.splice()和Array.slice()方法有什么区别
### 16、再说一下Computed和Watch
### 17、什么是观察者？
### 18、Vue中双向数据绑定是如何实现的？
### 19、nextTick知道吗，实现原理是什么？
### 20、如何在JavaScript中每x秒调用一个函数
### 21、Vue里面router-link在电脑上有用，在安卓上没反应怎么解决？
### 22、vue的实现原理？
### 23、什么是生命周期hook？列出一些生命周期hook。
### 24、JS 中的主要有哪几类错误
### 25、v-show和v-if指令的共同点和不同点？
### 26、vuex是什么？怎么使用？哪种功能场景使用它？
### 27、如何将 JS 日期转换为ISO标准
### 28、什么是动态 prop？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




