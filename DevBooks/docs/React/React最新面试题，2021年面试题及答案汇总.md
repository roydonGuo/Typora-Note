# React最新面试题，2022年面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、React与Vue的相似之处](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#1react与vue的相似之处)  


都使用 Virtual DOM

提供了响应式 (Reactive) 和组件化 (Composable) 的视图组件。

将注意力集中保持在核心库，而将其他功能如路由和全局状态管理交给相关的库。


### [2、Vue2.x和Vue3.x渲染器的diff算法分别说一下](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#2vue2x和vue3x渲染器的diff算法分别说一下)  


**简单来说，diff算法有以下过程**

**1、** 同级比较，再比较子节点

**2、** 先判断一方有子节点一方没有子节点的情况(如果新的children没有子节点，将旧的子节点移除)

**3、** 比较都有子节点的情况(核心diff)

**4、** 递归比较子节点

正常Diff两个树的时间复杂度是`O(n^3)`，但实际情况下我们很少会进行`跨层级的移动DOM`，所以Vue将Diff进行了优化，从`O(n^3) -> O(n)`，只有当新旧children都为多个子节点时才需要用核心的Diff算法进行同层级比较。

Vue2的核心Diff算法采用了`双端比较`的算法，同时从新旧children的两端开始进行比较，借助key值找到可复用的节点，再进行相关操作。相比React的Diff算法，同样情况下可以减少移动节点次数，减少不必要的性能损耗，更加的优雅。

Vue3.x借鉴了 [ivi](https://github.com/localvoid/ivi)算法和 [inferno](https://github.com/infernojs/inferno)算法

在创建VNode时就确定其类型，以及在`mount/patch`的过程中采用`位运算`来判断一个VNode的类型，在这个基础之上再配合核心的Diff算法，使得性能上较Vue2.x有了提升。(实际的实现可以结合Vue3.x源码看。)

该算法中还运用了`动态规划`的思想求解最长递归子序列。

(看到这你还会发现，框架内无处不蕴藏着数据结构和算法的魅力)

**面试官：(可以可以，看来是个苗子，不过自我介绍属实有些无聊，下一题)**


### [3、概述下 React 中的事件处理逻辑](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#3概述下-react-中的事件处理逻辑)  


为了解决跨浏览器兼容性问题`React` 会将浏览器原生事件`Browser Native Event`封装为合成事件`SyntheticEvent`传入设置的事件处理器中。这里的合成事件提供了与原生事件相同的接口不过它们屏蔽了底层浏览器的细节差异保证了行为的一致性。另外有意思的是React 并没有直接将事件附着到子元素上而是以单一事件监听器的方式将所有的事件发送到顶层进行处理。这样 `React` 在更新 `DOM` 的时候就不需要考虑如何去处理附着在 `DOM` 上的事件监听器最终达到优化性能的目的


### [4、再说一下vue2.x中如何监测数组变化](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#4再说一下vue2x中如何监测数组变化)  


使用了函数劫持的方式，重写了数组的方法，Vue将data中的数组进行了原型链重写，指向了自己定义的数组原型方法。这样当调用数组api时，可以通知依赖更新。如果数组中包含着引用类型，会对数组中的引用类型再次递归遍历进行监控。这样就实现了监测数组变化。

（能问到这的面试官都比较注重深度，这些常规操作要记牢）


### [5、React组件通信如何实现?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#5react组件通信如何实现)  


**React组件间通信方式:**

**1、** 父组件向子组件通讯: 父组件可以向子组件通过传 props 的方式，向子组件进行通讯

**2、** 子组件向父组件通讯: props+回调的方式,父组件向子组件传递props进行通讯，此props为作用域为父组件自身的函数，子组件调用该函数，将子组件想要传递的信息，作为参数，传递到父组件的作用域中

**3、** 兄弟组件通信: 找到这两个兄弟节点共同的父节点,结合上面两种方式由父节点转发信息进行通信

**4、** 跨层级通信: `Context`设计目的是为了共享那些对于一个组件树而言是“全局”的数据，例如当前认证的用户、主题或首选语言,对于跨越多层的全局数据通过`Context`通信再适合不过

**5、** 发布订阅模式: 发布者发布事件，订阅者监听事件并做出反应,我们可以通过引入event模块进行通信

**6、** 全局状态管理工具: 借助Redux或者Mobx等全局状态管理工具进行通信,这种工具会维护一个全局状态中心Store,并根据不同的事件产生新的状态

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/4/30/1939/39/97_2.png#alt=97%5C_2.png)


### [6、React Portal 有哪些使用场景](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#6react-portal-有哪些使用场景)  


在以前 `react` 中所有的组件都会位于 `#app` 下而使用 `Portals` 提供了一种脱离 `#app` 的组件因此 `Portals` 适合脱离文档流(`out of flow`) 的组件特别是 `position: absolute` 与 `position: fixed`的组件。比如模态框通知警告`goTop` 等。

以下是官方一个模态框的示例可以在以下地址中测试效果

```
<html>
  <body>
    <div id="app"></div>
    <div id="modal"></div>
    <div id="gotop"></div>
    <div id="alert"></div>
  </body>
</html>
```

```
const modalRoot = document.getElementById('modal');

class Modal extends React.Component {
  constructor(props) {
    super(props);
    this.el = document.createElement('div');
  }

  componentDidMount() {
    modalRoot.appendChild(this.el);
  }

  componentWillUnmount() {
    modalRoot.removeChild(this.el);
  }

  render() {
    return ReactDOM.createPortal(
      this.props.children,
      this.el,
    );
  }
}
```

`React Hooks`当中的`useEffect`是如何区分生命周期钩子的

`useEffect`可以看成是`componentDidMountcomponentDidUpdate`和`componentWillUnmount`三者的结合。`useEffect(callback, [source])`接收两个参数调用方式如下

```
 useEffect(() => {
   console.log('mounted');
   
   return () => {
       console.log('willUnmount');
   }
 }, [source]);
```

生命周期函数的调用主要是通过第二个参数[source]来进行控制有如下几种情况

**1、** [source]参数不传时则每次都会优先调用上次保存的函数中返回的那个函数然后再调用外部那个函数

**2、** [source]参数传[]时则外部的函数只会在初始化时调用一次返回的那个函数也只会最终在组件卸载时调用一次

**3、** [source]参数有值时则只会监听到数组中的值发生变化后才优先调用返回的那个函数再调用外部的函数。


### [7、你能用HOC做什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#7你能用hoc做什么)  


**HOC可用于许多任务，例如：**

**1、** 代码重用，逻辑和引导抽象

**2、** 渲染劫持

**3、** 状态抽象和控制

**4、** Props 控制


### [8、Store 在 Redux 中的意义是什么？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#8store-在-redux-中的意义是什么)  


Store 是一个 JavaScript 对象，它可以保存程序的状态，并提供一些方法来访问状态、调度操作和注册侦听器。应用程序的整个状态/对象树保存在单一存储中。因此，Redux 非常简单且是可预测的。我们可以将中间件传递到 store 来处理数据，并记录改变存储状态的各种操作。所有操作都通过 reducer 返回一个新状态。


### [9、区分Real DOM和Virtual DOM](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#9区分real-dom和virtual-dom)  

| Real DOM | Virtual DOM |
| --- | --- |
| 1、更新缓慢。 | 1、更新更快。 |
| 2、可以直接更新 HTML。 | 2、无法直接更新 HTML。 |
| 3、如果元素更新，则创建新DOM。 | 3、如果元素更新，则更新 JSX 。 |
| 4、DOM操作代价很高。 | 4、DOM 操作非常简单。 |
| 5、消耗的内存较多。 | 5、很少的内存消耗。 |



### [10、那你能讲一讲MVVM吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题，2021年面试题及答案汇总.md#10那你能讲一讲mvvm吗)  


MVVM是`Model-View-ViewModel`缩写，也就是把`MVC`中的`Controller`演变成`ViewModel`。Model层代表数据模型，View代表UI组件，ViewModel是View和Model层的桥梁，数据会绑定到viewModel层并自动将数据渲染到页面中，视图变化的时候会通知viewModel层更新数据。


### 11、你都做过哪些Vue的性能优化？
### 12、你了解 Virtual DOM 吗？解释一下它的工作原理。
### 13、说一下v-model的原理
### 14、什么是控制组件？
### 15、为什么虚拟dom会提高性能
### 16、react性能优化是哪个周期函数
### 17、hash路由和history路由实现原理说一下
### 18、什么是React 路由？
### 19、Redux 有哪些优点？
### 20、列出 React Router 的优点。
### 21、nextTick知道吗，实现原理是什么？
### 22、如何更新组件的状态？
### 23、在合成事件 和 生命周期钩子(除 componentDidUpdate) 中setState是"异步"的
### 24、组件中的data为什么是一个函数？
### 25、shouldComponentUpdate 的作用
### 26、与 ES5 相比，React 的 ES6 语法有何不同？
### 27、React 中 keys的作用是什么





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




