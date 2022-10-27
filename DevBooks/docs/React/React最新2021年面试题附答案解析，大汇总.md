# React最新2022年面试题附答案解析，大汇总


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、React中的状态是什么？它是如何使用的？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#1react中的状态是什么它是如何使用的)  


状态是 React 组件的核心，是数据的来源，必须尽可能简单。基本上状态是确定组件呈现和行为的对象。与props 不同，它们是可变的，并创建动态和交互式组件。可以通过 `this.state()` 访问它们。


### [2、connect原理](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#2connect原理)  


首先`connect`之所以会成功是因为`Provider`组件在原应用组件上包裹一层使原来整个应用成为`Provider`的子组件接收`Redux`的`store`作为`props`通过`context`对象传递给子孙组件上的`connect`connect做了些什么。它真正连接 `Redux`和 `React`它包在我们的容器组件的外一层它接收上面 `Provider` 提供的 `store` 里面的`state` 和 `dispatch`传给一个构造函数返回一个对象以属性形式传给我们的容器组件

`connect`是一个高阶函数首先传入mapStateToProps、mapDispatchToProps然后返回一个生产Component的函数(wrapWithConnect)然后再将真正的Component作为参数传入wrapWithConnect这样就生产出一个经过包裹的Connect组件该组件具有如下特点

通过`props.store`获取祖先`Component`的`store props`包括`stateProps`、`dispatchProps`、`parentProps`,合并在一起得到`nextState`作为`props`传给真正的`Component componentDidMount`时添加事件`this.store.subscribe(this.handleChange)`实现页面交互`shouldComponentUpdate`时判断是否有避免进行渲染提升页面性能并得到nextState componentWillUnmount时移除注册的事件`this.handleChange`

由于connect的源码过长我们只看主要逻辑

```
export default function connect(mapStateToProps, mapDispatchToProps, mergeProps, options = {}) {
  return function wrapWithConnect(WrappedComponent) {
    class Connect extends Component {
      constructor(props, context) {
        // 从祖先Component处获得store
        this.store = props.store || context.store
        this.stateProps = computeStateProps(this.store, props)
        this.dispatchProps = computeDispatchProps(this.store, props)
        this.state = { storeState: null }
        // 对stateProps、dispatchProps、parentProps进行合并
        this.updateState()
      }
      shouldComponentUpdate(nextProps, nextState) {
        // 进行判断当数据发生改变时Component重新渲染
        if (propsChanged 
        || mapStateProducedChange 
        || dispatchPropsChanged) {
          this.updateState(nextProps)
            return true
          }
        }
        componentDidMount() {
          // 改变Component的state
          this.store.subscribe(() = {
            this.setState({
              storeState: this.store.getState()
            })
          })
        }
        render() {
          // 生成包裹组件Connect
          return (
            <WrappedComponent {...this.nextState} />
          )
        }
      }
      Connect.contextTypes = {
        store: storeShape
      }
      return Connect;
    }
  }
```


### [3、react hooks它带来了那些便利](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#3react-hooks它带来了那些便利)  


**1、** 代码逻辑聚合逻辑复用

**2、** `HOC`嵌套地狱

**3、** 代替 `class`

**4、** `React` 中通常使用 类定义 或者 函数定义 创建组件:

在类定义中我们可以使用到许多 `React` 特性例如 `state`、 各种组件生命周期钩子等但是在函数定义中我们却无能为力因此 `React 16.8` 版本推出了一个新功能 (`React Hooks`)通过它可以更好的在函数定义组件中使用 `React` 特性。

**好处:**

**1、** 跨组件复用: 其实 `render` `props` / `HOC` 也是为了复用相比于它们Hooks 作为官方的底层 `API`最为轻量而且改造成本小不会影响原来的* 组件层次结构和传说中的嵌套地狱

**2、** 类定义更为复杂

**3、** 不同的生命周期会使逻辑变得分散且混乱不易维护和管理

**4、** 时刻需要关注 `this`的指向问题

**5、** 代码复用代价高高阶组件的使用经常会使整个组件树变得臃肿

**6、** 状态与UI隔离: 正是由于 `Hooks` 的特性状态逻辑会变成更小的粒度并且极容易被抽象成一个自定义 `Hooks`组件中的状态和 `UI` 变得更为清晰和隔离。

注意:

避免在 循环/条件判断/嵌套函数 中调用 `hooks`保证调用顺序的稳定只有 函数定义组件 和 `hooks` 可以调用 `hooks`避免在 类组件 或者 普通函数 中调用不能在`useEffect`中使用`useStateReact` 会报错提示类组件不会被替换或废弃不需要强制改造类组件两种方式能并存重要钩子

状态钩子 (`useState`): 用于定义组件的`State`其到类定义中`this.state`的功能

```
// useState 只接受一个参数: 初始状态
// 返回的是组件名和更改该组件对应的函数
const [flag, setFlag] = useState(true);
// 修改状态
setFlag(false)
 
// 上面的代码映射到类定义中:
this.state = {
 flag: true 
}
const flag = this.state.flag
const setFlag = (bool) => {
    this.setState({
        flag: bool,
    })
}
```


### [4、setState到底是异步还是同步?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#4setstate到底是异步还是同步)  


先给出答案: 有时表现出异步,有时表现出同步

**1、** `setState`只在合成事件和钩子函数中是“异步”的在原生事件和`setTimeout` 中都是同步的

**2、** `setState` 的“异步”并不是说内部由异步代码实现其实本身执行的过程和代码都是同步的只是合成事件和钩子函数的调用顺序在更新之前导致在合成事件和钩子函数中没法立马拿到更新后的值形成了所谓的“异步”当然可以通过第二个参数`setState(partialState, callback)`中的`callback`拿到更新后的结果

**3、** `setState` 的批量更新优化也是建立在“异步”合成事件、钩子函数之上的在原生事件和`setTimeout` 中不会批量更新在“异步”中如果对同一个值进行多次`setState`的批量更新策略会对其进行覆盖取最后一次的执行如果是同时`setState`多个不同的值在更新时会对其进行合并批量更新


### [5、什么是高阶组件（HOC）？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#5什么是高阶组件hoc)  


高阶组件是重用组件逻辑的高级方法，是一种源于 React 的组件模式。 HOC 是自定义组件，在它之内包含另一个组件。它们可以接受子组件提供的任何动态，但不会修改或复制其输入组件中的任何行为。你可以认为 HOC 是“纯（Pure）”组件。


### [6、setState到底是异步还是同步?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#6setstate到底是异步还是同步)  


先给出答案: 有时表现出异步,有时表现出同步

**1、** `setState`只在合成事件和钩子函数中是“异步”的，在原生事件和`setTimeout` 中都是同步的

**2、** `setState` 的“异步”并不是说内部由异步代码实现，其实本身执行的过程和代码都是同步的，只是合成事件和钩子函数的调用顺序在更新之前，导致在合成事件和钩子函数中没法立马拿到更新后的值，形成了所谓的“异步”，当然可以通过第二个参数 `setState(partialState, callback)` 中的`callback`拿到更新后的结果

**3、** `setState` 的批量更新优化也是建立在“异步”（合成事件、钩子函数）之上的，在原生事件和setTimeout 中不会批量更新，在“异步”中如果对同一个值进行多次`setState`，`setState`的批量更新策略会对其进行覆盖，取最后一次的执行，如果是同时`setState`多个不同的值，在更新时会对其进行合并批量更新


### [7、React有哪些限制？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#7react有哪些限制)  


**React的限制如下：**

**1、**  React 只是一个库，而不是一个完整的框架

**2、**  它的库非常庞大，需要时间来理解

**3、**  新手程序员可能很难理解

**4、**  编码变得复杂，因为它使用内联模板和 JSX


### [8、redux的工作流程?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#8redux的工作流程)  


首先，我们看下几个核心概念：

**1、** Store：保存数据的地方，你可以把它看成一个容器，整个应用只能有一个Store。

**2、** State：Store对象包含所有数据，如果想得到某个时点的数据，就要对Store生成快照，这种时点的数据集合，就叫做State。

**3、** Action：State的变化，会导致View的变化。但是，用户接触不到State，只能接触到View。所以，State的变化必须是View导致的。Action就是View发出的通知，表示State应该要发生变化了。

**4、** Action Creator：View要发送多少种消息，就会有多少种Action。如果都手写，会很麻烦，所以我们定义一个函数来生成Action，这个函数就叫Action Creator。

**5、** Reducer：Store收到Action以后，必须给出一个新的State，这样View才会发生变化。这种State的计算过程就叫做Reducer。Reducer是一个函数，它接受Action和当前State作为参数，返回一个新的State。

**6、** dispatch：是View发出Action的唯一方法。

**然后我们过下整个工作流程：**

**1、** 首先，用户（通过View）发出Action，发出方式就用到了dispatch方法。

**2、** 然后，Store自动调用Reducer，并且传入两个参数：当前State和收到的Action，Reducer会返回新的State

**3、** State一旦有变化，Store就会调用监听函数，来更新View。

到这儿为止，一次用户交互流程结束。可以看到，在整个流程中数据都是单向流动的，这种方式保证了流程的清晰。

![](https://gitee.com/souyunkutech/souyunku-home/raw/master/images/souyunku-web/2020/4/30/1939/39/97_11.png#alt=97%5C_11.png)


### [9、你是如何理解fiber的?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#9你是如何理解fiber的)  


React Fiber 是一种基于浏览器的**单线程调度算法**.

React 16之前 ，`reconcilation` 算法实际上是递归，想要中断递归是很困难的，React 16 开始使用了循环来代替之前的递归.

`Fiber`：**一种将 `recocilation` （递归 diff），拆分成无数个小任务的算法；它随时能够停止，恢复。停止恢复的时机取决于当前的一帧（16ms）内，还有没有足够的时间允许计算。**


### [10、diff算法?](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题附答案解析，大汇总.md#10diff算法)  


**1、** 把树形结构按照层级分解只比较同级元素。

**2、** 给列表结构的每个单元添加唯一的key属性方便比较。

**3、** `React` 只会匹配相同 `class` 的 `component`这里面的class指的是组件的名字

**4、** 合并操作调用 `component` 的 `setState` 方法的时候, React 将其标记为 - `dirty`.到每一个事件循环结束, `React` 检查所有标记 `dirty`的 `component`重新绘制.

**5、** 选择性子树渲染。开发人员可以重写 `shouldComponentUpdate`提高 `diff`的性能


### 11、Redux三大原则
### 12、你对 Time Slice的理解?
### 13、React 中的箭头函数是什么？怎么用？
### 14、为什么要用redux
### 15、keep-alive了解吗
### 16、什么是React？
### 17、详细解释 React 组件的生命周期方法。
### 18、虚拟DOM实现原理?
### 19、React中的合成事件是什么？
### 20、列出一些应该使用 Refs 的情况。
### 21、再说一下虚拟Dom以及key属性的作用
### 22、React的请求应该放在哪个生命周期中?
### 23、React 中 key 的重要性是什么？
### 24、React中的事件是什么？
### 25、Redux实现原理解析
### 26、HOC(高阶组件)
### 27、在生命周期中的哪一步你应该发起 AJAX 请求
### 28、SSR了解吗？





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




