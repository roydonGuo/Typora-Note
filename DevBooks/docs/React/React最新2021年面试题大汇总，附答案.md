# React最新2022年面试题大汇总，附答案


### 全部答案，更新日期：2022年5月18日，直接下载吧！

### 下载链接：[高清172份，累计 7701 页大厂面试题  PDF](https://gitee.com/souyunku/DevBooks/blob/master/docs/index.md)



### [1、你的接口请求一般放在哪个生命周期中？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#1你的接口请求一般放在哪个生命周期中)  


接口请求一般放在`mounted`中，但需要注意的是服务端渲染时不支持mounted，需要放到`created`中。


### [2、如何在 Redux 中定义 Action？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#2如何在-redux-中定义-action)  


React 中的 Action 必须具有 type 属性，该属性指示正在执行的 ACTION 的类型。必须将它们定义为字符串常量，并且还可以向其添加更多的属性。在 Redux 中，action 被名为 Action Creators 的函数所创建。以下是 Action 和Action Creator 的示例：

```
function addTodo(text) {
       return {
                type: ADD_TODO,
                 text
    }
}
```


### [3、如何在 React 中创建表单](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#3如何在-react-中创建表单)  


React 表单类似于 HTML 表单。但是在 React 中，状态包含在组件的 state 属性中，并且只能通过 `setState()` 更新。因此元素不能直接更新它们的状态，它们的提交是由 JavaScript 函数处理的。此函数可以完全访问用户输入到表单的数据。

```
handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
}

render() {
    return (
        <form onSubmit={this.handleSubmit}>
            <label>
                Name:
                <input type="text" value={this.state.value} onChange={this.handleSubmit} />
            </label>
            <input type="submit" value="Submit" />
        </form>
    );
}
```


### [4、你对 React 的 refs 有什么了解？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#4你对-react-的-refs-有什么了解)  


Refs 是 React 中引用的简写。它是一个有助于存储对特定的 React 元素或组件的引用的属性，它将由组件渲染配置函数返回。用于对 render() 返回的特定元素或组件的引用。当需要进行 DOM 测量或向组件添加方法时，它们会派上用场。

```
class ReferenceDemo extends React.Component{
     display() {
         const name = this.inputDemo.value;
         document.getElementById('disp').innerHTML = name;
     }
render() {
    return(
          <div>
            Name: <input type="text" ref={input => this.inputDemo = input} />
            <button name="Click" onClick={this.display}>Click</button>
            <h2>Hello <span id="disp"></span> !!!</h2>
          </div>
    );
   }
 }
```


### [5、我现在有一个button要用react在上面绑定点击事件要怎么做](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#5我现在有一个button要用react在上面绑定点击事件要怎么做)  


```
class Demo {
  render() {
    return <button onClick={(e) => {
      alert('我点击了按钮')
    }}>
      按钮
    </button>
  }
}
```

你觉得你这样设置点击事件会有什么问题吗

由于`onClick`使用的是匿名函数所有每次重渲染的时候会把该`onClick`当做一个新的prop来处理会将内部缓存的`onClick`事件进行重新赋值所以相对直接使用函数来说可能有一点的性能下降

修改

```
class Demo {

  onClick = (e) => {
    alert('我点击了按钮')
  }

  render() {
    return <button onClick={this.onClick}>
      按钮
    </button>
  }
```


### [6、说说你用react有什么坑点](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#6说说你用react有什么坑点)  


**1、** JSX做表达式判断时候需要强转为boolean类型

如果不使用 !!b 进行强转数据类型会在页面里面输出 0。

```
render() {
  const b = 0;
  return <div>
    {
      !!b && <div>这是一段文本</div>
    }
  </div>
}
```

**1、** 尽量不要在 `componentWillReviceProps` 里使用 `setState`如果一定要使用那么需要判断结束条件不然会出现无限重渲染导致页面崩溃

**2、** 给组件添加ref时候尽量不要使用匿名函数因为当组件更新的时候匿名函数会被当做新的`prop`处理让`ref`属性接受到新函数的时候`react`内部会先清空`ref`也就是会以`null`为回调参数先执行一次`ref`这个`props`然后在以该组件的实例执行一次`ref`所以用匿名函数做ref的时候有的时候去`ref`赋值后的属性会取到`null`

**3、** 遍历子节点的时候不要用 index 作为组件的 key 进行传入


### [7、setState](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#7setstate)  


在了解`setState`之前我们先来简单了解下 `React` 一个包装结构: `Transaction`:

**事务 (Transaction)**

是 `React` 中的一个调用结构用于包装一个方法结构为: `initialize` - `perform(method)` - `close`。通过事务可以统一管理一个方法的开始与结束处于事务流中表示进程正在执行一些操作


### [8、为什么需要 React 中的路由？](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#8为什么需要-react-中的路由)  


Router 用于定义多个路由，当用户定义特定的 URL 时，如果此 URL 与 Router 内定义的任何 “路由” 的路径匹配，则用户将重定向到该特定路由。所以基本上我们需要在自己的应用中添加一个 Router 库，允许创建多个路由，每个路由都会向我们提供一个独特的视图

```
<switch>
    <route exact path=’/’ component={Home}/>
    <route path=’/posts/:id’ component={Newpost}/>
    <route path=’/posts’   component={Post}/>
</switch>
```


### [9、pureComponent和FunctionComponent区别](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#9purecomponent和functioncomponent区别)  


`PureComponent`和`Component`完全相同但是在`shouldComponentUpdate`实现中`PureComponent`使用了`props`和`state`的浅比较。主要作用是用来提高某些特定场景的性能


### [10、react旧版生命周期函数](https://gitee.com/souyunku/DevBooks/blob/master/docs/React/React最新2021年面试题大汇总，附答案.md#10react旧版生命周期函数)  


初始化阶段

**1、** `getDefaultProps`:获取实例的默认属性

**2、** `getInitialState`:获取每个实例的初始化状态

**3、** `componentWillMount`组件即将被装载、渲染到页面上

**4、** `render`:组件在这里生成虚拟的DOM节点

**5、** `componentDidMount`:组件真正在被装载之后

运行中状态

**1、** `componentWillReceiveProps`:组件将要接收到属性的时候调用

**2、** `shouldComponentUpdate`:组件接受到新属性或者新状态的时候可以返回 `false`接收数据后不更新阻止 `render`调用后面的函数不会被继续执行了

**3、** `componentWillUpdate`:组件即将更新不能修改属性和状态

**4、** `render`:组件重新描绘

**5、** `componentDidUpdate`:组件已经更新


### 11、diff算法?
### 12、mixin、hoc、render props、react-hooks的优劣如何？
### 13、React与Angular有何不同？
### 14、列出React的一些主要优点。
### 15、如何在React中创建一个事件？
### 16、createElement 与 cloneElement 的区别是什么
### 17、再说一下Computed和Watch
### 18、react-router里的标签和`<a>`标签有什么区别
### 19、简述flux 思想
### 20、传入 setState 函数的第二个参数的作用是什么
### 21、什么是 Props?
### 22、React如何进行组件/逻辑复用?
### 23、为什么浏览器无法读取JSX？
### 24、setState到底是异步还是同步?
### 25、Redux设计理念
### 26、什么是纯组件？
### 27、React有哪些优化性能是手段?
### 28、react 的虚拟dom是怎么实现的





## [全部答案，更新日期：2022年5月18日，直接下载吧！](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)

### 下载链接：[全部答案，整理好了](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




## [新增：高清PDF：172份，7701页，最新整理](https://gitee.com/souyunku/DevBooks/blob/master/docs/daan.md)




