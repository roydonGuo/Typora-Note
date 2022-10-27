# React最新面试题2022年，常见面试题及答案汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、React 中 refs 的作用是什么](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#1react-中-refs-的作用是什么)  


`Refs` 是 `React` 提供给我们的安全访问 `DOM`元素或者某个组件实例的句柄可以为元素添加ref属性然后在回调函数中接受该元素在 `DOM` 树中的句柄该值会作为回调函数的第一个参数返回


### [2、区分状态和 props](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#2区分状态和-props)  

| 条件 | State | Props |
| --- | --- | --- |
| 1、从父组件中接收初始值 | Yes | Yes |
| 2、父组件可以改变值 | No | Yes |
| 3、在组件中设置默认值 | Yes | Yes |
| 4、在组件的内部变化 | Yes | No |
| 5、设置子组件的初始值 | Yes | Yes |
| 6、在子组件的内部更改 | No | Yes |



### [3、什么是Redux？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#3什么是redux)  


Redux 是当今最热门的前端开发库之一。它是 JavaScript 程序的可预测状态容器，用于整个应用的状态管理。使用 Redux 开发的应用易于测试，可以在不同环境中运行，并显示一致的行为。


### [4、React的请求应该放在哪个生命周期中?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#4react的请求应该放在哪个生命周期中)  


React的异步请求到底应该放在哪个生命周期里,有人认为在`componentWillMount`中可以提前进行异步请求,避免白屏,其实这个观点是有问题的.

由于JavaScript中异步事件的性质，当您启动API调用时，浏览器会在此期间返回执行其他工作。当React渲染一个组件时，它不会等待componentWillMount它完成任何事情 - React继续前进并继续render,没有办法“暂停”渲染以等待数据到达。

而且在`componentWillMount`请求会有一系列潜在的问题,首先,在服务器渲染时,如果在 componentWillMount 里获取数据，fetch data会执行两次，一次在服务端一次在客户端，这造成了多余的请求,其次,在React 16进行React Fiber重写后,`componentWillMount`可能在一次渲染中多次调用.

目前官方推荐的异步请求是在`componentDidmount`中进行.

如果有特殊需求需要提前请求,也可以在特殊情况下在`constructor`中请求:

> react 17之后`componentWillMount`会被废弃,仅仅保留`UNSAFE_componentWillMount`



### [5、列出 Redux 的组件。](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#5列出-redux-的组件。)  


Redux 由以下组件组成：

**1、**  Action – 这是一个用来描述发生了什么事情的对象。

**2、**  Reducer – 这是一个确定状态将如何变化的地方。

**3、**  Store – 整个程序的状态/对象树保存在Store中。

**4、**  View – 只显示 Store 提供的数据。


### [6、redux异步中间件之间的优劣?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#6redux异步中间件之间的优劣)  


**redux-thunk优点:**

**1、** 体积小: redux-thunk的实现方式很简单,只有不到20行代码

**2、** 使用简单: redux-thunk没有引入像redux-saga或者redux-observable额外的范式,上手简单

**redux-thunk缺陷:**

**1、** 样板代码过多: 与redux本身一样,通常一个请求需要大量的代码,而且很多都是重复性质的

**2、** 耦合严重: 异步操作与redux的action偶合在一起,不方便管理

**3、** 功能孱弱: 有一些实际开发中常用的功能需要自己进行封装

**redux-saga优点:**

**1、** 异步解耦: 异步操作被被转移到单独 saga.js 中，不再是掺杂在 action.js 或 component.js 中

**2、** action摆脱thunk function: dispatch 的参数依然是一个纯粹的 action (FSA)，而不是充满 “黑魔法” thunk function

**3、** 异常处理: 受益于 generator function 的 saga 实现，代码异常/请求失败 都可以直接通过 try/catch 语法直接捕获处理

**4、** 功能强大: redux-saga提供了大量的Saga 辅助函数和Effect 创建器供开发者使用,开发者无须封装或者简单封装即可使用

**5、** 灵活: redux-saga可以将多个Saga可以串行/并行组合起来,形成一个非常实用的异步flow

**6、** 易测试，提供了各种case的测试方案，包括mock task，分支覆盖等等

**redux-saga缺陷:**

**1、** 额外的学习成本: redux-saga不仅在使用难以理解的 generator function,而且有数十个API,学习成本远超redux-thunk,最重要的是你的额外学习成本是只服务于这个库的,与redux-observable不同,redux-observable虽然也有额外学习成本但是背后是rxjs和一整套思想

**2、** 体积庞大: 体积略大,代码近2000行，min版25KB左右

**3、** 功能过剩: 实际上并发控制等功能很难用到,但是我们依然需要引入这些代码

**4、** ts支持不友好: yield无法返回TS类型

**redux-observable优点:**

**1、** 功能最强: 由于背靠rxjs这个强大的响应式编程的库,借助rxjs的操作符,你可以几乎做任何你能想到的异步处理

**2、** 背靠rxjs: 由于有rxjs的加持,如果你已经学习了rxjs,redux-observable的学习成本并不高,而且随着rxjs的升级redux-observable也会变得更强大

**redux-observable缺陷:**

学习成本奇高: 如果你不会rxjs,则需要额外学习两个复杂的库

社区一般: redux-observable的下载量只有redux-saga的1/5,社区也不够活跃,在复杂异步流中间件这个层面redux-saga仍处于领导地位



### [7、如何模块化 React 中的代码？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#7如何模块化-react-中的代码)  


可以使用 export 和 import 属性来模块化代码。它们有助于在不同的文件中单独编写组件。

```
//ChildComponent.jsx
export default class ChildComponent extends React.Component {
    render() {
        return(
              <div>
                  <h1>This is a child component</h1>
              </div>
        );
    }
}

//ParentComponent.jsx
import ChildComponent from './childcomponent.js';
class ParentComponent extends React.Component {
    render() {
        return(
             <div>
                <App />
             </div>
        );
    }
}
```


### [8、redux中间件有哪些，做什么用？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#8redux中间件有哪些做什么用)  


中间件提供第三方插件的模式，自定义拦截 action -> reducer 的过程。变为 action -> middlewares -> reducer 。这种机制可以让我们改变数据流，实现如异步 action ，action 过滤，日志输出，异常报告等功能。 常见的中间件：

redux-logger：提供日志输出

redux-thunk：处理异步操作

redux-promise：处理异步操作，actionCreator的返回值是promise


### [9、那你知道Vue3.x响应式数据原理吗？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#9那你知道vue3x响应式数据原理吗)  


(还好我有看，这个难不倒我)

Vue3.x改用`Proxy`替代Object.defineProperty。因为Proxy可以直接监听对象和数组的变化，并且有多达13种拦截方法。并且作为新标准将受到浏览器厂商重点持续的性能优化。

**Proxy只会代理对象的第一层，那么Vue3又是怎样处理这个问题的呢？**

判断当前Reflect.get的返回值是否为Object，如果是则再通过`reactive`方法做代理， 这样就实现了深度观测。

**监测数组的时候可能触发多次get/set，那么如何防止触发多次呢？**

我们可以判断key是否为当前被代理对象target自身属性，也可以判断旧值与新值是否相等，只有满足以上两个条件之一时，才有可能执行trigger。

面试官抬起了头。心里暗想

(这小子还行，比上两个强，应该是多多少少看过Vue3的源码了)


### [10、你对“单一事实来源”有什么理解？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新面试题2021年，常见面试题及答案汇总.md#10你对“单一事实来源有什么理解)  


Redux 使用 “Store” 将程序的整个状态存储在同一个地方。因此所有组件的状态都存储在 Store 中，并且它们从 Store 本身接收更新。单一状态树可以更容易地跟踪随时间的变化，并调试或检查程序。


### 11、redux的工作流程?
### 12、区分有状态和无状态组件。
### 13、销毁阶段
### 14、React组件通信如何实现？
### 15、虚拟DOM的优劣如何?
### 16、Vue2.x组件通信有哪些方式？
### 17、如何将两个或多个组件嵌入到一个组件中？
### 18、react性能优化方案
### 19、什么是JSX？
### 20、MVC框架的主要问题是什么？
### 21、React Router与常规路由有何不同？
### 22、解释一下 Flux
### 23、react-redux是如何工作的?
### 24、什么是高阶组件(HOC)
### 25、React有什么特点？
### 26、说一下Vue的生命周期
### 27、redux中如何进行异步操作?





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




