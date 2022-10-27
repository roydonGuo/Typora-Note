# React最新2022年面试题，高级面试题及附答案解析


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、React组件生命周期的阶段是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#1react组件生命周期的阶段是什么)  


React 组件的生命周期有三个不同的阶段：

**1、** 初始渲染阶段：这是组件即将开始其生命之旅并进入 DOM 的阶段。

**2、** 更新阶段：一旦组件被添加到 DOM，它只有在 prop 或状态发生变化时才可能更新和重新渲染。这些只发生在这个阶段。

**3、** 卸载阶段：这是组件生命周期的最后阶段，组件被销毁并从 DOM 中删除。


### [2、Redux与Flux有何不同？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#2redux与flux有何不同)  

| Flux | Redux |
| --- | --- |
| 1、Store 包含状态和更改逻辑 | 1、Store 和更改逻辑是分开的 |
| 2、有多个 Store | 2、只有一个 Store |
| 3、所有 Store 都互不影响且是平级的 | 3、带有分层 reducer 的单一 Store |
| 4、有单一调度器 | 4、没有调度器的概念 |
| 5、React 组件订阅 store | 5、容器组件是有联系的 |
| 6、状态是可变的 | 6、状态是不可改变的 |



### [3、React实现的移动应用中如果出现卡顿有哪些可以考虑的优化方案](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#3react实现的移动应用中如果出现卡顿有哪些可以考虑的优化方案)  


**1、** 增加`shouldComponentUpdate`钩子对新旧`props`进行比较如果值相同则阻止更新避免不必要的渲染或者使用`PureReactComponent`替代`Component`其内部已经封装了`shouldComponentUpdate`的浅比较逻辑

**2、** 对于列表或其他结构相同的节点为其中的每一项增加唯一`key`属性以方便`React`的`diff`算法中对该节点的复用减少节点的创建和删除操作

render函数中减少类似

```
onClick={() => {
    doSomething()
}}
```

的写法每次调用`render`函数时均会创建一个新的函数即使内容没有发生任何变化也会导致节点没必要的重渲染建议将函数保存在组件的成员对象中这样只会创建一次

**1、** 组件的props如果需要经过一系列运算后才能拿到最终结果则可以考虑使用`reselect`库对结果进行缓存如果props值未发生变化则结果直接从缓存中拿避免高昂的运算代价

**2、** webpack-bundle-analyzer分析当前页面的依赖包是否存在不合理性如果存在找到优化点并进行优化


### [4、Redux遵循的三个原则是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#4redux遵循的三个原则是什么)  


**1、**  单一事实来源：整个应用的状态存储在单个 store 中的对象/状态树里。单一状态树可以更容易地跟踪随时间的变化，并调试或检查应用程序。

**2、**  状态是只读的：改变状态的唯一方法是去触发一个动作。动作是描述变化的普通 JS 对象。就像 state 是数据的最小表示一样，该操作是对数据更改的最小表示。

**3、**  使用纯函数进行更改：为了指定状态树如何通过操作进行转换，你需要纯函数。纯函数是那些返回值仅取决于其参数值的函数。


### [5、简单说一下Vue2.x响应式数据原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#5简单说一下vue2x响应式数据原理)  


Vue在初始化数据时，会使用`Object.defineProperty`重新定义data中的所有属性，当页面使用对应属性时，首先会进行依赖收集(收集当前组件的`watcher`)如果属性发生变化会通知相关依赖进行更新操作(`发布订阅`)。


### [6、如何告诉 React 它应该编译生产环境版](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#6如何告诉-react-它应该编译生产环境版)  


通常情况下我们会使用 `Webpack` 的 `DefinePlugin` 方法来将 `NODE_ENV` 变量值设置为 `production`。编译版本中 `React`会忽略 `propType` 验证以及其他的告警信息同时还会降低代码库的大小React 使用了 `Uglify` 插件来移除生产环境下不必要的注释等信息


### [7、React最新的生命周期是怎样的?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#7react最新的生命周期是怎样的)  


React 16之后有三个生命周期被废弃(但并未删除)

**1、** componentWillMount

**2、** componentWillReceiveProps

**3、** componentWillUpdate

官方计划在17版本完全删除这三个函数，只保留UNSAVE_前缀的三个函数，目的是为了向下兼容，但是对于开发者而言应该尽量避免使用他们，而是使用新增的生命周期函数替代它们

目前React 16.8 +的生命周期分为三个阶段,分别是挂载阶段、更新阶段、卸载阶段

**挂载阶段:**

**1、** constructor: 构造函数，最先被执行,我们通常在构造函数里初始化state对象或者给自定义方法绑定this

**2、** getDerivedStateFromProps: `static getDerivedStateFromProps(nextProps, prevState)`,这是个静态方法,当我们接收到新的属性想去修改我们state，可以使用getDerivedStateFromProps

**3、** render: render函数是纯函数，只返回需要渲染的东西，不应该包含其它的业务逻辑,可以返回原生的DOM、React组件、Fragment、Portals、字符串和数字、Boolean和null等内容

**4、** componentDidMount: 组件装载之后调用，此时我们可以获取到DOM节点并操作，比如对canvas，svg的操作，服务器请求，订阅都可以写在这个里面，但是记得在componentWillUnmount中取消订阅

**更新阶段:**

**1、** getDerivedStateFromProps: 此方法在更新个挂载阶段都可能会调用

**2、** shouldComponentUpdate: `shouldComponentUpdate(nextProps, nextState)`,有两个参数nextProps和nextState，表示新的属性和变化之后的state，返回一个布尔值，true表示会触发重新渲染，false表示不会触发重新渲染，默认返回true,我们通常利用此生命周期来优化React程序性能

**3、** render: 更新阶段也会触发此生命周期

**4、** getSnapshotBeforeUpdate: `getSnapshotBeforeUpdate(prevProps, prevState)`,这个方法在render之后，componentDidUpdate之前调用，有两个参数prevProps和prevState，表示之前的属性和之前的state，这个函数有一个返回值，会作为第三个参数传给componentDidUpdate，如果你不想要返回值，可以返回null，此生命周期必须与componentDidUpdate搭配使用

**5、** componentDidUpdate: `componentDidUpdate(prevProps, prevState, snapshot)`,该方法在getSnapshotBeforeUpdate方法之后被调用，有三个参数prevProps，prevState，snapshot，表示之前的props，之前的state，和snapshot。第三个参数是getSnapshotBeforeUpdate返回的,如果触发某些回调函数时需要用到 DOM 元素的状态，则将对比或计算的过程迁移至 getSnapshotBeforeUpdate，然后在 componentDidUpdate 中统一触发回调或更新状态。

**卸载阶段:**

componentWillUnmount: 当我们的组件被卸载或者销毁了就会调用，我们可以在这个函数里去清除一些定时器，取消网络请求，清理无效的DOM元素等垃圾清理工作

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/4/30/1939/39/97_1.png#alt=97%5C_1.png)


### [8、Vue事件绑定原理说一下](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#8vue事件绑定原理说一下)  


原生事件绑定是通过`addEventListener`绑定给真实元素的，组件事件绑定是通过Vue自定义的`$on`实现的。

**面试官：(这小子基础还可以，接下来我得上上难度了)**


### [9、Vue中组件生命周期调用顺序说一下](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#9vue中组件生命周期调用顺序说一下)  


**1、** 组件的调用顺序都是`先父后子`,渲染完成的顺序是`先子后父`。

**2、** 组件的销毁操作是`先父后子`，销毁完成的顺序是`先子后父`。

**加载渲染过程**

`父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount- >子mounted->父mounted`

**子组件更新过程**

`父beforeUpdate->子beforeUpdate->子updated->父updated`

**父组件更新过程**

`父 beforeUpdate -> 父 updated`

**销毁过程**

`父beforeDestroy->子beforeDestroy->子destroyed->父destroyed`


### [10、react 的渲染过程中兄弟节点之间是怎么处理的也就是key值不一样的时候](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题，高级面试题及附答案解析.md#10react-的渲染过程中兄弟节点之间是怎么处理的也就是key值不一样的时候)  


通常我们输出节点的时候都是`map`一个数组然后返回一个`ReactNode`为了方便`react`内部进行优化我们必须给每一个`reactNode`添加`key`这个`key prop`在设计值处不是给开发者用的而是给react用的大概的作用就是给每一个reactNode添加一个身份标识方便react进行识别在重渲染过程中如果key一样若组件属性有所变化则`react`只更新组件对应的属性没有变化则不更新如果`key`不一样则`react`先销毁该组件然后重新创建该组件


### 11、说一下v-if和v-show的区别
### 12、为什么选择使用框架而不是原生?
### 13、React如何进行组件/逻辑复用?
### 14、react组件的划分业务组件技术组件
### 15、你对受控组件和非受控组件了解多少？
### 16、redux中间件
### 17、redux与mobx的区别?
### 18、redux有什么缺点
### 19、react和vue的区别
### 20、解释 React 中 render() 的目的。
### 21、解释 Reducer 的作用。
### 22、为什么React Router v4中使用 switch 关键字 ？
### 23、setState: React 中用于修改状态更新视图。它具有以下特点:
### 24、你理解“在React中，一切都是组件”这句话。
### 25、你对 Time Slice的理解?
### 26、Vue模版编译原理知道吗，能简单说一下吗？
### 27、生命周期钩子 (useEffect):
### 28、具体实现步骤如下





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




