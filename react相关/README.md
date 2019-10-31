# React相关知识

## 一、react入门
### 背景
React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram 的网站。做出来以后，发现这套东西很好用，就在2013年5月开源了。
### 什么是React
- A JAVASCRIPT LIBRARY FOR BUILDING USER INTERFACES
 
    - 用来构建UI的 JavaScript库
    - React 不是一个 MVC 框架，仅仅是视图（V）层的库
- [React 官网](https://reactjs.org/)
- [React 中文文档](https://react.docschina.org/)

###  特点
- 使用 JSX语法 创建组件，实现组件化开发，为函数式的 UI 编程方式打开了大门
- 性能高的让人称赞：通过 [diff算法](https://zh-hans.reactjs.org/docs/reconciliation.html#the-diffing-algorithm) 和 [虚拟DOM](https://zh-hans.reactjs.org/docs/faq-internals.html#what-is-the-virtual-dom) 实现视图的高效更新

### 为什么要用React

- 1 使用组件化开发方式，符合现代Web开发的趋势
- 2 技术成熟，社区完善，配件齐全，适用于大型Web项目（生态系统健全）
- 3 由Facebook专门的团队维护，技术支持可靠
- 4 ReactNative - Learn once, write anywhere: Build mobile apps with React
- 5 使用方式简单，性能非常高，支持服务端渲染
- 6 React非常火，从技术角度，可以满足好奇心，提高技术水平

### React的基本使用

Create React App （本文推荐使用官方脚手架）是一个用于学习 React 的舒适环境，也是用 React 创建新的单页应用的最佳方式。

```
npx create-react-app my-app
cd my-app
npm start


目录结构

├── public                  # webpack的配置的静态目录
│   ├── favicon.ico
│   ├── index.html          # 首页模板，默认是单页面应用，这个是最终的html的基础模板
│   └── manifest.json       # 如果是一个 app 定义 app 的图标 网址 主题颜色等
├── src                     #项目所有的源代码
│   ├── App.css             # App根组件的css
│   ├── App.js              # App组件代码
│   ├── App.test.js
│   ├── index.css           # 启动文件样式
│   ├── index.js            # 整个程序的入口 (react 的理念 all in js)
│   ├── logo.svg
│   └── serviceWorker.js    #将网页存储在浏览器内 如果突然断网了 可以继续访问该网页　　(PWD progressive web application 借助写来的 网页 用来做 app)
├── package.json            #node 的包文件 和项目介绍 （ 命令行 命令 ） 等
└── yarn.lock               #依赖的安装包 （一般不用动）

 
```
### JSX 的基本使用

- 注意：[JSX语法](https://react.docschina.org/docs/introducing-jsx.html)，最终会被编译为 createElement() 方法
- 推荐：使用 JSX 的方式创建组件
- JSX - JavaScript XML
#### JSX注意点
- 1: 如果在 JSX 中给元素添加类, 需要使用 className 代替 class
    - 类似：label 的 for属性，使用htmlFor代替
- 2：在 JSX 中可以直接使用 JS代码，直接在 JSX 中通过 {} 中间写 JS代码即可
- 3：在 JSX 中只能使用表达式，但是不能出现 语句！！！
- 4：在 JSX 中注释语法：{/* 中间是注释的内容 */}

示例代码：

```
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
### 组件
- 组件允许你将 UI 拆分为独立可复用的代码片段，并对每个片段进行独立构思。
- 组件，从概念上类似于 JavaScript 函数。它接受任意的入参（即 “props”），并返回用于描述页面展示内容的 React 元素。

#### React创建组件的两种方式
- 通过 JS函数 创建（无状态组件）
- 通过 class 创建（有状态组件）

```
函数式组件 和 class 组件的使用场景说明：
1、 如果一个组件仅仅是为了展示数据，那么此时就可以使用 函数组件
2、 如果一个组件中有一定业务逻辑，需要操作数据，那么就需要使用 class 创建组件，因为，此时需要使用 state
```

####  JavaScript 函数

```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
该函数是一个有效的 React 组件，因为它接收唯一带有数据的 “props”（代表属性）对象与并返回一个 React 元素。这类组件被称为“函数组件”，因为它本质上就是 JavaScript 函数。

#### class创建

```
//  react对象继承字React.Component
class Welcome extends React.Component {
// class创建的组件中 必须有rander方法 且显示return一个react对象或者null
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
### props和state
#### props
- 作用：给组件传递数据，一般用在父子组件之间
- 说明：React把传递给组件的属性转化为一个对象并交给 props
- 特点：props是只读的，无法给props添加或修改属性
- props.children：获取组件的内容，比如：
    - <Hello>组件内容</Hello> 中的 组件内容

```
// props 是一个包含数据的对象参数，不要试图修改 props 参数
// 返回值：react元素
function Welcome(props) {
  // 返回的 react元素中必须只有一个根元素
  return <div>hello, {props.name}</div>
}

class Welcome extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    return <h1>Hello, {this.props.name}</h1>
  }
}
```
#### state

```
状态即数据
```
- 作用：用来给组件提供组件内部使用的数据
- 注意：只有通过class创建的组件才具有状态
- 注意：状态是私有的，完全由组件来控制
- 注意：不要在 state 中添加 render() 方法中不需要的数据，会影响渲染性能！
- 
- 可以将组件内部使用但是不渲染在视图中的内容，直接添加给 this
- 注意：不要在 render() 方法中调用 setState() 方法来修改state的值

```
class Hello extends React.Component {
  constructor() {
    // es6继承必须用super调用父类的constructor
    super()

    this.state = {
      name: '张三'
    }
  }

  render() {
    return (
      <div>姓名：{ this.state.name }</div>
    )
  }
}
```
### 组件的生命周期
每个组件都包含“生命周期方法”，你可以重写这些方法，以便于在运行过程中特定的阶段执行这些方法。你可以使用此[生命周期图谱](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)作为速查表。在下述列表中，常用的生命周期方法会被加粗。其余生命周期函数的使用则相对罕见。


#### 挂载
当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下：
- **constructor()**：初始化 state ，进行方法绑定
- static getDerivedStateFromProps()：会在调用 render 方法之前调用，并且在初始挂载及后续更新时都会被调用。它应返回一个对象来更新 state，如果返回 null 则不更新任何内容。
- **render()**：是 class 组件中唯一必须实现的方法，应该为纯函数。
- **componentDidMount()**：组件挂载后（插入 DOM 树中）立即调用，**网络请求**在此发出
#### 更新
当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下：
- static getDerivedStateFromProps()
- shouldComponentUpdate()：当 props 或 state 发生变化时，会在渲染执行之前被调用
- **render()**：重新渲染组件
- getSnapshotBeforeUpdate()：在最近一次渲染输出（提交到 DOM 节点）之前调用。它使得组件能在发生更改之前从 DOM 中捕获一些信息（例如，滚动位置）。此生命周期的任何返回值将作为参数传递给 componentDidUpdate()
- **componentDidUpdate()**：在更新后会被立即调用，首次渲染不会执行此方法
#### 卸载
当组件从 DOM 中移除时会调用如下方法：
- **componentWillUnmount()**：会在组件卸载及销毁之前直接调用。在此方法中执行必要的清理操作，例如，清除 timer，取消网络请求。
#### 错误处理
当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法：
- static getDerivedStateFromError()：此生命周期会在后代组件抛出错误后被调用。 它将抛出的错误作为参数，并返回一个值以更新 state
- componentDidCatch()：此生命周期在后代组件抛出错误后被调用。

### 组件绑定事件
- 1 **通过React事件机制 onClick 绑定（推荐）**
- 2 JS原生方式绑定（通过 ref 获取元素）
    - 注意：ref 是React提供的一个特殊属性
    - ref的使用说明：[react ref](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html#___gatsby)

```
例如：onClick 用来绑定单击事件
<input type="button" value="触发单击事件"
  onClick={this.handleCountAdd}
  onMouseEnter={this.handleMouseEnter}
/>
```
## 二、react-router

[react-router 官网](https://reacttraining.com/react-router/)
（[中文文档](http://react-guide.github.io/react-router-cn/index.html)）

### 简介
React Router 是一个基于 React 之上的强大路由库，它可以让你向应用中快速地添加视图和数据流，同时保持页面与 URL 间的同步。

### 使用步骤
- 1 导入路由组件
- 2 使用 <Router></Router> 作为根容器，包裹整个应用（JSX）
    - 在整个应用程序中，只需要使用一次
- 3 使用 <Link to="/movie"></Link> 作为链接地址，并指定to属性
- 4 使用 <Route path="/" compoent={Movie}></Route> 展示路由内容

### 注意点
- <Router></Router>：作为整个组件的根元素，是路由容器，只能有一个唯一的子元素
- <Link></Link>：类似于vue中的<router-link></router-link>标签，to 属性指定路由地址
- <Route></Route>：类似于vue中的<router-view></router-view>，指定路由内容（组件）展示位置

### 路由参数
- 配置：通过Route中的path属性来配置路由参数
- 获取：this.props.match.params 获取

### 路由跳转
- react router - [history](https://reacttraining.com/react-router/web/api/history)
- history.push() 方法用于在JS中实现页面跳转
- history.go(-1) 用来实现页面的前进（1）和后退(-1)


## 三、redux
[Redux 中文文档](https://www.redux.org.cn/)

### 设计思想
Redux 的设计思想很简单，就两句话。

```
（1）Web 应用是一个状态机，视图与状态是一一对应的。

（2）所有的状态，保存在一个对象里面。
```
### 基本概念和 API
#### Store
Store 就是保存数据的地方，你可以把它看成一个容器。整个应用只能有一个 Store。

Redux 提供createStore这个函数，用来生成 Store。

```
import { createStore } from 'redux';
const store = createStore(fn);
```
上面代码中，createStore函数接受另一个函数作为参数，返回新生成的 Store 对象。
Store 有以下职责：
- 维持应用的 state；
- 提供 getState() 方法获取 state；
- 提供 dispatch(action) 方法更新 state；
- 通过 subscribe(listener) 注册监听器;
- 通过 subscribe(listener) 返回的函数注销监听器（执行 subscribe 返回的函数即可）。

#### State

Store对象包含所有数据。如果想得到某个时点的数据，就要对 Store 生成快照。这种时点的数据集合，就叫做 State。

当前时刻的 State，可以通过store.getState()拿到。

Redux 规定， 一个 State 对应一个 View。只要 State 相同，View 就相同。你知道 State，就知道 View 是什么样，反之亦然。

#### Action
State 的变化，会导致 View 的变化。但是，用户接触不到 State，只能接触到 View。所以，State 的变化必须是 View 导致的。Action 就是 View 发出的通知，表示 State 应该要发生变化了。

Action 是一个对象。其中的type属性是必须的，表示 Action 的名称。其他属性可以自由设置，社区有一个[规范](https://github.com/redux-utilities/flux-standard-action)可以参考。

Action 是把数据从应用（译者注：这里之所以不叫 view 是因为这些数据有可能是服务器响应，用户输入或其它非 view 的数据 ）传到 store 的有效载荷。它是 store 数据的唯一来源。一般来说你会通过 store.dispatch() 将 action 传到 store。

```
const action = {
  type: 'ADD_TODO',
  payload: 'Learn Redux'
};

store.dispatch(action);
```
上面代码中，Action 的名称是ADD_TODO，它携带的信息是字符串Learn Redux。

可以这样理解，Action 描述当前发生的事情。改变 State 的唯一办法，就是使用 Action。它会运送数据到 Store。
#### Reducer
Reducers 指定了应用状态的变化如何响应 actions 并发送到 store 的，记住 actions 只是描述了有事情发生了这一事实，并没有描述应用如何更新 state。

Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State。


```
const defaultState = 0;
const reducer = (state = defaultState, action) => {
  switch (action.type) {
    case 'ADD':
      return state + action.payload;
    default: 
      return state;
  }
};

const state = reducer(1, {
  type: 'ADD',
  payload: 2
});
```
上面代码中，reducer函数收到名为ADD的 Action 以后，就返回一个新的 State，作为加法的计算结果。其他运算的逻辑（比如减法），也可以根据 Action 的不同来实现。

实际应用中，Reducer 函数不用像上面这样手动调用，store.dispatch方法会触发 Reducer 的自动执行。为此，Store 需要知道 Reducer 函数，做法就是在生成 Store 的时候，将 Reducer 传入createStore方法。

```
import { createStore } from 'redux';
const store = createStore(reducer);
```
上面代码中，createStore接受 Reducer 作为参数，生成一个新的 Store。以后每当store.dispatch发送过来一个新的 Action，就会自动调用 Reducer，得到新的 State。

通过combineReducers函数将多个拆分的reducer合并

#### 工作流程
![image](http://www.ruanyifeng.com/blogimg/asset/2016/bg2016091802.jpg)

首先，用户发出 Action。

```
store.dispatch(action);
```
然后，Store 自动调用 Reducer，并且传入两个参数：当前 State 和收到的 Action。 Reducer 会返回新的 State 。

```
let nextState = todoApp(previousState, action);
```
State 一旦有变化，Store 就会调用监听函数。

```
// 设置监听函数
store.subscribe(listener);
```
listener可以通过store.getState()得到当前状态。如果使用的是 React，这时可以触发重新渲染 View。
```
function listerner() {
  let newState = store.getState();
  component.setState(newState);   
}
```

## 四、React-Redux
为了方便使用，Redux 的作者封装了一个 React 专用的库 [React-Redux](https://github.com/reactjs/react-redux)

### 容器组件和展示组件

|         | 展示组件    |  容器组件   
| --------    | ----- | ----  |
| 作用      | 描述如何展现（骨架、样式）  |  描述如何运行（数据获取、状态更新）   |
| 直接使用 Redux        |  否  |  是   |
| 数据来源        |    props  |   监听 Redux state  |
|数据修改   | 从 props 调用回调函数 | 向 Redux 派发 actions
| 调用方式 | 手动 | 通常由 React Redux 
### connect()
React-Redux 提供connect方法，用于从 UI 组件生成容器组件。connect的意思，就是将这两种组件连起来。


```
connect(mapStateToProps,mapDispatchToProps)
```
前者负责输入逻辑，即将state映射到 UI 组件的参数（props）;

后者负责输出逻辑，即将用户对 UI 组件的操作映射成 Action。
- （1）输入逻辑：外部的数据（即state对象）如何转换为 UI 组件的参数
- （2）输出逻辑：用户发出的动作如何变为 Action 对象，从 UI 组件传出去。

```
import { connect } from 'react-redux'
import { increment, decrement, reset } from './actionCreators'

// const Counter = ...

const mapStateToProps = (state /*, ownProps*/) => {
  return {
    counter: state.counter
  }
}

const mapDispatchToProps = { increment, decrement, reset }

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(Counter)
```
装饰器模式
> @connect(
mapStateToProps,
mapDispatchToProps
)

### Provider
connect方法生成容器组件以后，需要让容器组件拿到state对象，才能生成 UI 组件的参数。

一种解决方法是将state对象作为参数，传入容器组件。但是，这样做比较麻烦，尤其是容器组件可能在很深的层级，一级级将state传下去就很麻烦。

React-Redux 提供Provider组件，可以让容器组件拿到state。


```
import React from 'react'
import ReactDOM from 'react-dom'
import { Provider } from 'react-redux'
import store from './store'
import App from './App'

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```
## 五、Redux-saga
[redux-saga](https://redux-saga-in-chinese.js.org/) 是一个用于管理应用程序 Side Effect（副作用，例如异步获取数据，访问浏览器缓存等）的 library，它的目标是让副作用管理更容易，执行更高效，测试更简单，在处理故障时更容易。

它没有把异步操作放在 action creator 中，也没有去处理 reductor，而是把所有的异步操作看成“线程”，可以通过普通的action去触发它，当操作完成时也会触发action作为输出。saga 的意思本来就是一连串的事件。

redux-saga 使用了 ES6 的 [Generator](http://es6.ruanyifeng.com/#docs/generator) 功能，让异步的流程更易于读取，写入和测试。通过这样的方式，这些异步的流程看起来就像是标准同步的 Javascript 代码。

直接看例子：

```
// saga.js
import { take, put } from 'redux-saga/effects'

function* mySaga(){ 
    // 阻塞: take方法就是等待 USER_INTERACTED_WITH_UI_ACTION 这个 action 执行
    yield take(USER_INTERACTED_WITH_UI_ACTION);
    
    // 阻塞: put方法将同步发起一个 action
    yield put(SHOW_LOADING_ACTION, {isLoading: true});
    
    // 阻塞: 将等待 FetchFn 结束，等待返回的 Promise
    const data = yield call(FetchFn, 'https://my.server.com/getdata');
    
    // 阻塞: 将同步发起 action (使用刚才返回的 Promise.then)
    yield put(SHOW_DATA_ACTION, {data: data});
}
```
这里用了好几个yield，简单理解，也就是每个 yield 都发起了阻塞，saga 会等待执行结果返回，再执行下一指令。也就是相当于take、put、call、put 这几个方法的调用变成了同步的，上面的全部完成返回了，才会执行下面的，类似于 await。

### 相关API
##### createSagaMiddleware()
创建一个 Redux middleware，并将 Sagas 连接到 Redux Store。

##### middleware.run(saga, ...args)
动态地运行 saga。只能 用于在 applyMiddleware 阶段 之后 执行 Saga。

- saga: Function: 一个 Generator 函数
- args: Array<any>: 提供给 saga 的参数

##### takeEvery(pattern, saga, ...args)
在发起（dispatch）到 Store 并且匹配 pattern 的每一个 action 上派生一个 saga。
- pattern: String | Array | Function - 有关更多信息，请参见 take(pattern) 的文档
- saga: Function - 一个 Generator 函数
- args: Array<any> - 传递给启动任务的参数。takeEvery 会把当前的 action 追加到参数列表中。（即 action 将是 saga 的最后一个参数）

##### takeLatest(pattern, saga, ...args)
在发起到 Store 并且匹配 pattern 的每一个 action 上派生一个 saga。并自动取消之前所有已经启动但仍在执行中的 saga 任务。

##### takeLeading(pattern, saga, ...args)

在发起到 Store 并且匹配 pattern 的每一个 action 上派生一个 saga。 它将在派生一次任务之后阻塞，直到派生的 saga 完成，然后又再次开始监听指定的 pattern。

##### take(pattern)
创建一个 Effect 描述信息，用来命令 middleware 在 Store 上等待指定的 action。 在发起与 pattern 匹配的 action 之前，Generator 将暂停。
##### put(action)
创建一个 Effect 描述信息，用来命令 middleware 向 Store 发起一个 action。 这个 effect 是非阻塞型的，并且所有向下游抛出的错误（例如在 reducer 中），都不会冒泡回到 saga 当中。

##### call(fn, ...args)
创建一个 Effect 描述信息，用来命令 middleware 以参数 args 调用函数 fn 。
##### fork(fn, ...args)
创建一个 Effect 描述信息，用来命令 middleware 以 非阻塞调用 的形式执行 fn。
用于管理 Saga 间并发的中心化 Effect。
yield fork(fn ...args) 的结果是一个 Task 对象 —— 一个具备着某些实用方法及属性的对象。

##### cancel(task)
创建一个 Effect 描述信息，用来命令 middleware 取消之前的一个分叉任务。
##### cancel(...tasks)
创建一个 Effect 描述信息，用来命令 middleware 取消之前的多个分叉任务。

##### select(selector, ...args)
创建一个 Effect，用来命令 middleware 在当前 Store 的 state 上调用指定的选择器（即返回 selector(getState(), ...args) 的结果）。
- selector: Function - 一个 (state, ...args) => args 的函数。它接受当前 state 和一些可选参数，并返回当前 Store state 上的一部分数据。

如果调用 select 的参数为空（即 yield select()），那么 effect 会取得完整的 state（与调用 getState() 的结果相同）。