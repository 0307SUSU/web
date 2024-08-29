# jsx

> 声明react元素
>
> jsx语法转译后会变成react创建Element的一个方法`React.creactElement('p',null,'hello world!')`
>
> jsx语法最外层只能有一个标签
>
> jsx语法中的所有标签必须闭合，就是在结尾加上'/'
>
> jsx中可以随意使用js表达式，唯一需要注意的是js表达式需要用大括号包裹
>
> 属性命名必须以驼峰命名方式命名
>
> jsx中行内样式以对象形式书写，属性名以驼峰式命名
>
> 注释要用{}包裹，像这样：{/*\*我是jsx注释*\*/}
>
> 定义事件onClick={事件或者事件名}
>
> jsx语法可以防止xss攻击

```jsx
const name = "我是jsx";
{/*下面定义了一个h1元素*/}
// 定义一个事件
function handleClick(){
    console.log('我是h1标签');
}
const element = <h1 className="titleStyle" onClick={handleClick} style={{fontSize:'18px'}}>你好{name}</h1>;
```



# 组件

> react中组件可以理解为可复用的模块，分为两种：函数组件和类组件

## 函数组件

> 本质上就是一个js函数，接受了一个props对象做为参数，并返回jsx
>
> 

```jsx
// 定义函数并接收props
function Button(props){
    
    return (
        // 返回jsx
    	<div>
        	<h1>{props.name}</h1>
        </div>
    )
}
// 使用函数组件
const btn = <Button name="function按钮" />;
```



## 类组件

> 类组件基于es6的class语法创建
>
> 拥有状态state，可以使用生命周期函数

```jsx
// 定义一个类
class Button extends React.Component {
    // 通过render方法返回jsx
    render(){
        return (
        <div>
        	<h1>{this.props.name}</h1>
        </div>
        )
    }
}
const btn = <Button name="class按钮"/>;
```

### 生命周期

> react的生命周期一般分为三个阶段，挂载(组件被渲染成真实DOM时调用)、更新(组件的状态或props发生变化时调用)、卸载(组件从DOM中移除时调用)

```jsx
// 生命周期函数包括
1. cosntructor(){}
2. componentWillMount(){}
3. render(){}
4. componentDidMount(){}
5. componentWillUnmount(){}

1. componentWillReceiveProps(){}
2. shouldComponentUpdate(){}
3. componentWillUpdate(){}
4. componentDidUpdate(){}
```



## state

> 组件内部管理的数据，决定了组件最终渲染结果，状态可以改变
>
> this.setState 更新state
>
> 函数组件和类组件中使用状态的方式不同

```jsx
// 类组件
class Button extends React.Component{
    // 定义内部状态
    constructor(props){
        super(props);
        this.state = {
            date: new Date()
        }
    }
    
    formatteTime(){
        const getTime = this.state.date.getTime();
        // 改变状态
        this.setState({
            date: getTime
        });
    }
    
    render(){
        // 渲染jsx
        return (
        <div>
        	<h2>当前时间是: {this.state.date}</h2> 
            <h3 onClick={formatteTime}>转为时间戳格式</h3>
        </div>
        )
    }
}
```

```jsx
// 函数组件
/**
*注：函数组件本身没有状态，需要借助Hook才能在组件内使用状态（关于hook是什么，后续在作解释）
**/
import React, {useState} from 'react';  // 导入所需的hook

// 定义函数
function Button (props){
    const [date,setDate] = useState(new Date()); // 初始化状态数据
    
    function formatteTime(){
        const getTime = date.getTime();
        // 改变状态
        setDate(getTime);
    }
    
    return (
     <div>
        	<h2>当前时间是: {date}</h2> 
            <h3 onClick={formatteTime}>转为时间戳格式</h3>
      </div>
    )
}



```

## props

> 翻译：属性
>
> props是子组件接收父组件传递的数据，子组件不可以直接改变props
>
> 属性传递，可以传递任意类型的内容，

```jsx
function Button(props){
    // 返回jsx内容，并使用传递的props属性，
    return <button>{props.name}</button>
}

function Text(){
    return <span style={{color:'#ff6700'}}>带颜色的文字</span>
}

function App(){
    const value= "变量按钮"
    function handleClick(){
        console.log('函数执行')
    }
    return (
    	<div>
            {/*使用子组件，并为子组件传递name属性*/}
        	<Button name="字符串按钮" />
            {/*使用子组件，并传递变量*/}
            <Button name={value} />
            {/*传递函数*/}
            <Button name={handleClick} />
            {/*传递组件*/}
            <Button name={<Text/>} />
            {/*...*/}
        </div>
    )
}
```



## hooks

> 在 React 16.8 版本引入了 Hooks，在hooks引入之前函数组件是不能够使用状态和其它的一些react特性的，
>
> hooks主要用于函数组件，以扩展函数组件的功能
>
> hooks是函数方法，react内置了一些hooks，也可以自定义hooks，

```jsx
// 内置hooks
import React, {useState,useEffect} from 'react'; // 需要引入，用到哪个引哪个

// 1. useState()  状态管理

const [state,setState] = useState(initialState);  // 初始化状态，state是当前值，setstate是更新当前状态的函数，initialState是初始值（可以不写，默认输出undefined，所以最好是写上）


// 2. useEffect   处理副作用（所谓副作用，就是指组件除了渲染 UI 之外，还会对组件外部产生影响的操作），它基本包揽了类组件中的生命周期方法能做的任何操作,它接收两个参数，第一个参数为一个函数（作用是在函数中编写副作用逻辑），第二个参数为一个数组（作用是作为依赖项，当依赖项发生变化时useEffect才会重新执行，依赖项可以是一个空[],这时只在挂载时执行一次，也可以包含某个值，这时初始化时执行一次，当值发生变化时重新执行，相当于监听，也可以不写依赖项，不写依赖项每次渲染都会执行）。

// 函数式编程将那些跟数据计算无关的操作，都称为 "副效应" （side effect） 。如果函数内部直接包含产生副效应的操作，就不再是纯函数了，我们称之为不纯的函数。
// 一句话，钩子（hook）就是 React 函数组件的副效应解决方案，用来为函数组件引入副效应。 函数组件的主体只应该用来返回组件的 HTML 代码，所有的其他操作（副效应）都必须通过钩子引入。

// React 为许多常见的操作（副效应），都提供了专用的钩子。而 useEffect()是通用的副效应钩子 。找不到对应的钩子时，就可以用它。其实，从名字也可以看出来，它跟副效应（side effect）直接相关。

/*
只要是副效应，都可以使用useEffect()引入。它的常见用途有下面几种。

获取数据（data fetching）
事件监听或订阅（setting up a subscription）
改变 DOM（changing the DOM）
输出日志（logging）
*/

useEffect(()=>{
    console.log('只在挂载时执行一次')
},[])


const [name,setName] = useState('张三'); 
useEffect(()=>{
    console.log('挂载时执行一次，每次name变化时都会重新执行')
},[name])


useEffect(()=>{
    console.log('每次渲染后都执行，如果在useEffect中更新了组件的状态，而这个状态变化又会触发重新渲染，则可能会导致无限渲染循环。')
})


// useEffect()允许返回一个函数，在组件卸载时，执行该函数，清理副效应。如果不需要清理副效应，useEffect()就不用返回任何值。
useEffect(() => {
    //组件加载时订阅了一个事件
  const subscription = props.source.subscribe();
  return () => {
      // 返回一个清理函数，在组件卸载时取消订阅。
    subscription.unsubscribe();
  };
}, [props.source]);


// 3. useContext()   上下文
/*
	用于处理深层次的组件嵌套情况下底层组件无法直接读取顶层组件中的数据，只能通过props逐层传递才可以，例如a组件中有个id属性，在c组件中要用到，a和c之间隔了一个b，这时就需要先传参给b组件b再传参给c，只能逐层传递
	为了解决它，context出现了，它可以不通过b直接拿到a中的id，那么怎么做到的呢？往👇看
	首先我们承认react提供了一个方法处理它，就是usecontext(),具体怎么用我们将用法分成步骤
	1. 第一步我们要把a组件中的id传递给c，这时就要在a组件中引入一个api：createContext,在a组件中用createContext创建一个context并导出（没错要使用context必须要创建一个context）
	2. 创建完了context，我们要通过<context.provider value={}>组件包裹其引入的组件，将要传递的值赋值给value属性，这样就基本传递结束啦
    3. 接下来就是接收啦，当然哪里需要就在哪里接收喽，c组件需要就在c组件里接收，导入useContext钩子，然后再导入context，这里context是在a组件里创建的，就需要导入a组件拿到a组件导出的context，这里我们要拿到id，所以就在c组件中定义一个id常量，等于useContext(将创建的context放在这里就可以啦)。
    总结一下：其实就是创建一个context并导出，然后哪里需要就在哪里导入，使用时用useContext钩子取就可以啦，假如有一个a到e的嵌套组件，e中需要用到a中的id直接在e中导入a导出的context就可以啦（说得再多不如实际例子来的直观，别担心下边就展示代码示例）
*/

// 4. useReducer()   // 另一种状态管理方式
/*
	为什么要再搞一种状态管理方式？
	如果要处理的状态属性很多，使用useState去更新状态就会显得很杂乱无章，并且每处理一个状态就要调一次setstate，用usereducer可以解决处理复杂状态逻辑或多个状态更新步骤，先说一下概念在用实际例子证明
*/
// 我们用比较的方法来解释useReducer的用法，首先用useState实现一段代码，然后再用useReducer重新实现

// 用useState实现计数器
import React, { useState } from 'react';

// 定义一个count
const [count,setCount] = useState(0);
const Counter = () => {

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count+1)}>Increment</button>
      <button onClick={() => setCount(count-1)}>Decrement</button>
    </div>
  );
};

export default Counter;

// 用useReducer实现
import React, { useReducer } from 'react';

// 定义 reducer 函数
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error('Unknown action type');
  }
}

const Counter = () => {
  // 使用 useReducer Hook
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
};

export default Counter;
// 在这样一个简单的例子中看起来是useState用起来比较方便并且代码更加简洁，事实确实如此，如上所说useReducer更适合处理复杂逻辑和多状态更改，这里只是介绍两种不同用法，不用纠结哪个好记住一点，当你用useState处理状态感到很乱很繁琐时就用useReducer
/*
使用 useReducer 的场景
状态复杂度高: 当状态逻辑涉及多个子状态或复杂的状态更新规则时，useReducer 可以帮助保持代码的清晰性和可维护性。
状态共享: 在嵌套组件中，如果需要共享和管理相同的状态，useReducer 可以配合 Context API 使用。
*/

// 5. useMemo()  // 优化性能，计算属性，缓存计算结果
/*
它通过记住某个计算结果的值，只有在依赖项发生变化时才会重新计算，从而避免了不必要的计算。
它接受两个参数，一个返回计算结果的函数和一个执行函数的依赖项
还是一样，光有概念不行，得有实例
*/

// 还用count来举例，当count变化时span输出count加10后的值
import React,{useState,useMemo} from 'react'

const [count,setCount] = useState(0);
const cuntLog = useMemo(()=>{
    return count+10 
},[count]);
const counter = ()=>{
    return (
    	<button onClick={()=>setCount(count +1)}>加1</button>
        <span>{cuntLog}</span>
    )
};

export default counter;

// 在上面的例子看上去好像多此一举了，还不如直接在span里count+10，如果这样操作的话，每次页面重绘的时候都会执行一次count+10，如果是用useMemo就不会，因为它有缓存，他记住了上一次的计算结果，当页面重绘时，只要count没变他就不会去重新执行函数，直接返回之前的计算结果。当然向上面如此简单的计算，确实没必要使用useMemo,那么什么情况下才使用呢？
/*
只有在计算非常昂贵或组件渲染频繁时才考虑使用 useMemo，否则可能带来不必要的复杂性。
useMemo 的常见用途
复杂计算: 如过滤、排序、数学计算等。
优化渲染: 在依赖项不变的情况下，防止子组件因父组件重渲染而重复渲染。
避免重复对象创建: 如果某个对象的创建依赖复杂逻辑，可以用 useMemo 来记忆该对象。
*/

// 6. useCallback()  // 优化性能，缓存回调函数
/*
它的作用是记忆（缓存）一个回调函数，只有当依赖项发生变化时，才会重新生成该函数。这在传递回调函数给子组件或避免不必要的重新渲染时非常有用。闲话少说直接上例子
*/

import React, { useState, useEffect, useCallback } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  const fetchData = useCallback(async () => {
    const response = await fetch('https://api.example.com/data');
    const result = await response.json();
    setData(result);
  }, []);

  useEffect(() => {
    fetchData();
  }, [fetchData]);

  return (
    <div>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
};

export default DataFetcher;
//在这个例子中，fetchData 是一个异步函数，用于获取数据。useCallback 确保这个函数在 useEffect 中只在依赖项改变时重新创建（也就是fetchData函数改变时，比如请求地址变了），从而避免不必要的网络请求。

// 7. useRef() 
// ...
```

# React Router

> 路由可以干什么？
>  页面跳转
>  重定向、嵌套路由、路由传参、动态路由、编程式导航、延迟加载、路由守卫、代码分割、懒加载、索引路由

## 安装

> react路由是一个库，所以需要安装

```bash
npm i react-router-dom
```

## 核心组件

- BrowserRouter 提供路由功能,被它包裹的组件才有路由功能，一般用来包裹最顶层组件App

- routes  
- route 定义路由规则，说白了就是你要跳到那个组件去就要用他指定那个组件，并给那个组件加一个路径path
- link 创建导航链接，说白了就是你要跳到那个路由要通过它
- switch  包裹一组 Route 组件
- Outlet     出口
- navlink    动态链接

## 基本用法

> 首先理解一下基本用法要用它干什么？那一定是用于组件间的跳转了，比如有两个组件，一个是首页，首页中有一个去登录的按钮，点击后去登录组件，那么如果不用路由的话这个点击按钮的事件中该怎么实现跳转？那一定是利用windows原生的方法获取到登陆组件的路径地址，然后将这个地址push到浏览器的地址栏中实现跳转(这里不具体介绍原生实现的细节)，那么从原生实现方式可以搞清楚就是通过改变地址栏路径地址实现的组件跳转，那放在router中怎么实现？
>
> 分析：
>
> 要实现跳转首先得获取必要的元素，假设这两个组件都已经创建好了，要实现跳转首先要明确往哪里跳，明确之后第一步要获取到目标组件的路径地址，拿到地址后触发跳转要将拿到的地址推送到地址栏中
>
> 1. router怎么获取组件路径地址
> 2. 怎么将地址更新到地址栏
>
> 其实路径地址根本不需要获取，因为组件是你自己定义的，它在哪里你自己再清楚不过了，在router中要为这些组件再加一个路由的路径，也就是映射，重新起个名，将路由的名称指向组件，上边介绍核心组件的时候已经提到了有一个Route组件就是专门干这事儿的，好了地址定义好了。接着第二步，要将地址更新到地址栏router提供了Link组件，这两个组件怎么用？先通过代码来体验一下

```jsx
// 组件是属于router的所以要通过router导入
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';
import Home from "./home.jsx"
function App() {
  return (
      {/*要想用router跳转必须要通过BrowserRouter包裹*/}
    <BrowserRouter>
      <nav>
          {/*link标签有一个属性to，这个属性的作用就是指定要跳转到的路由的路径*/}
        <Link to="/">Home</Link>
        <Link to="/login">login</Link>
      </nav>
      <Routes>
          {/*route组件的path属性就是为组件定义一个路由路径去映射组件，element属性用来指定要映射的组件，要映射的组件从哪来？通过导入*/}
        <Route path="/" element={<Home />} />
        <   
Route path="/about" element={<About />} />
      </Routes>
    </   
BrowserRouter>
  );
}
```

## 编程式导航（跳转）

> 什么是编程式跳转？
>
> 上边基本用法中实现了路由跳转，需要通过点击link组件实现，假如登录的时候用户点击了登录按钮这时后会判断是否登录成功，如果失败会提示登录失败，并要求再次输入密码，如果登录成功，就跳转到首页，那如何实现在登录成功后跳转到首页呢？像这种在代码逻辑中控制路由跳转的方式就叫编程式跳转
>
> 虽然 `<Link>` 组件是React Router提供的导航方式之一，但它主要用于在UI中呈现可点击的导航链接。在需要根据逻辑条件自动跳转的场景下，比如登录成功后，使用编程式导航（如 `useNavigate` 或 `history.push`）更为合适，因为它不需要用户交互，并且能够更灵活地控制跳转逻辑。

### 编程式跳转的方法

```jsx
/*
1. useNavigate()
2. useHistory()
这些钩子都由reactRouter提供
*/
import {useNavigate,useHistory } from 'react-router-dom';

function Login(){
    const navigate = useNavigate();
    
    const handleLogin = () =>{
        navigate('/home');  // 通过useNavigate方法
    }
    
    return <button onClick={handleLogin}>Login</button>;
}


function Login2() {
  const history = useHistory();

  const handleLogin = () => {
    // 登录逻辑
    if (loginSuccess) {
      history.push('/home');   // 通过useHistory方法
    }
  };

  return <button onClick={handleLogin}>Login</button>;
}


// 在类组件中使用 this.props.history.push
class Login extends React.Component {
  handleLogin = () => {
    // 登录逻辑
    if (loginSuccess) {
      this.props.history.push('/home');
    }
  };

  render() {
    return <button onClick={this.handleLogin}>Login</button>;
  }
}

```

## 嵌套路由

```jsx
import { BrowserRouter as Router, Routes, Route, Link, Outlet } from 'react-router-dom';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="users" element={<Users />}>
            {/*路由里边定义路由*/}
          <Route path=":id" element={<UserDetail />} />
        </Route>
      </Routes>
    </Router>
  );
}

function Home() {
  return <h2>Home Page</h2>;
}

function Users() {
  return (
    <div>
      <h2>Users List</h2>
      <ul>
        <li><Link to="1">User 1</Link></li>
        <li><Link to="2">User 2</Link></li>
      </ul>
      {/* 渲染子路由 */}
      <Outlet />
    </div>
  );
}

function UserDetail() {
  return <h3>User Detail Page</h3>;
}

export default App;
```

## 路由传参

> 路由传参很有必要，假如你在登录成功后得到了一个用户的id属性，并且登陆成功后页面跳转到了首页，首页中有一个接口需要用到这个id，这时候你要怎么得到它？通过props吗？但是首页组件并没有在登陆组件中使用，所以无法通过props，这时候就可以用路由传参的方式，怎么用？

```jsx
```

## 动态路由

# Redux

> Store、createStore()
>
> State、store.getState()
>
> Action   store.dispatch()
>
> Reducer()
>
> store.subscribe()
>
> applyMiddlewares()
>
> 中间件
>
> 实在有些复杂，待后续再深入学习

```jsx
// 一个简单的store实例
const Counter = ({ value, onIncrement, onDecrement }) => (
  <div>
  <h1>{value}</h1>
  <button onClick={onIncrement}>+</button>
  <button onClick={onDecrement}>-</button>
  </div>
);

const reducer = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT': return state + 1;
    case 'DECREMENT': return state - 1;
    default: return state;
  }
};

const store = createStore(reducer);

const render = () => {
  ReactDOM.render(
    <Counter
      value={store.getState()}
      onIncrement={() => store.dispatch({type: 'INCREMENT'})}
      onDecrement={() => store.dispatch({type: 'DECREMENT'})}
    />,
    document.getElementById('root')
  );
};

render();
store.subscribe(render);
```

# 实战

> 前面学了那么多react的知识，还没有一点实战呢！，甚至还不知道真正创建一个react项目要怎么搞...前边学的怎么样先不管啦，老子要实操啦，md耶稣来了都拦不住我要实操！！！

> 上来就给俺干懵了！md该干啥？实际工作中开一个新项目投入开发时要干啥？一头雾水。。。

```bash
# 分析一波先
# 假如我要做一个餐饮管理系统的后台，需求和ui都定好了，要投入开发了，我要选框架呀（技术选型），用啥开发？那当然是react了，不然上边白学了。那就需要创建一个react项目，怎么创建？k上边没学呀...,问题不大，暂停，去学一下。
```

## 创建react项目

> **npx create-react-app react-app**   官方脚手架建法（创建好后配置好了一堆东西都不知道是干啥的，很不利于我后边的操作呀）
>
> npm 创建，npm install -g create-react-app在控制台用这个命令安装包，安装好后在执行create-react-app my-app，好啦创建了，（跟上边一样一堆东西不知道是干啥的）
>
> 使用webpack创建，这种创建方式完全就是所有东西全靠自己搞啊，不过正是我需要的，要啥就搞啥呗，不会去查，不靠脚手架生成

```bash
# 开始创建，首先在磁盘中创建一个项目文件夹

mkdir my-app
# 然后进入这个文件夹
cd my-app
# 进来之后初始化项目
npm init -y
#初始化完成啦，项目下面多了一个文件package.json。这是干嘛的？不会了去学一下 https://dev.nodejs.cn/learn/the-package-json-guide/
# 好啦，初始化也完成啦，接下来为写react代码做一些准备吧，首先是不是得有打包工具吧，安装打包工具，那么多打包工具要用哪一个呢？webpack or vite？这里用webpack吧，安装webpack依赖
npm i webpack webpack-cli webpack-dev-server --save-dev
#依赖安装完啦，创建webpack的配置文件(也有可能依赖安装完后会自动创建该文件，那就不用下边的命令啦)
type nul > webpack.config.js  # 关于webpack的配置不会去查
# 除了打包工具之外要写react代码还要安装可以运行react代码的依赖react&react-dom
npm install react react-dom
#react代码肯定是不能被浏览器识别的，那么就需要将它转化为浏览器能识别的js代码，所以还要安装一个依赖babel
npm i babel-loader @babel/core @babel/preset-env @babel/preset-react --save-dev
# 依赖安装完肯定要配置呀，所以在根目录下再创建一个文件.babelrc文件，关于它怎么配置的，不用多说去查吧
type nul > .babelrc
# 依赖安装的差不多啦，最初就先这样吧，然后代码写哪里呢？那当然是src文件夹下了，所以再创建一个src文件夹
mkdir src
# 至此就差不多啦，先把这些搞好后边再接着分析

```

### src文件夹

> 做完了上边的操作接下来就要关注代码写在哪里和怎么写了，首先肯定是写在src文件夹下，
>
> 然后怎么写呢？分析react，react是单文件组件，所以肯定要有一个.html文件，但是业务代码肯定不是写在这个文件下面，他只是用来接收和渲染react代码的文件，那么从哪接收呢，react肯定要有一个入口文件main.js，好那就创建这两个文件

- `index.html`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的react项目</title>
  </head>
  <body>
      <!--react代码输出的地方-->
    <div id="root"></div>
  </body>
  </html>
  
  ```

- `main.js`

  ```js
  import React from 'react'; // 导入react模块
  import ReactDOM from 'react-dom'; // 导入react-dom模块
  
  // 创建组件
  const App = () => {
    return <h1>Hello, React!</h1>;
  };
  
  // 将创建的react组件挂载到html文件的id为root的标签中
  ReactDOM.render(<App />, document.getElementById('root'));//React 18 以后的版本 render已弃用，新版本用下边的
  const root = ReactDOM.createRoot(document.getElementById('root'));
  root.render(<App />);
  ```

> 创建好文件之后按理说就可以了，但问题来了，怎么运行项目去浏览器中查看呢？
>
> 还需要去package.json中配置运行命令,添加完成后在控制台运行命令就可以啦

- `添加项目运行脚本`

  ```json
  "scripts": {
    "start": "webpack serve --mode development --open",
    "build": "webpack --mode production"
  }
  ```

> 当然在运行命令之前首先要确定前边的webpack配置文件已经配置好了，如果没有配置，那接下来就先配置好再去运行命令吧

- 配置webpack

  ```js
  const path = require('path'); // 导入nodejs的path模块
  const HtmlWebpackPlugin = require('html-webpack-plugin'); // 安装并导入HtmlWebpackPlugin插件
  
  /*
  首先基本了解一下webpack的配置，
  有5个核心模块，entry（入口）、output（出口）、loader、plugin(插件)、devServer
  想要正常运行项目，最基本的要配置入口
  */
  module.exports = {
    entry: './src/index.js', // 配置入口
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'bundle.js',
    },
    module: {
      rules: [
        {
          test: /\.(js|jsx)$/,
          exclude: /node_modules/,
          use: 'babel-loader',
        },
      ],
    },
    resolve: {
      extensions: ['.js', '.jsx'],
    },
    plugins: [
      new HtmlWebpackPlugin({
        template: './src/index.html',
      }),
    ],
    devServer: {
      contentBase: path.join(__dirname, 'dist'),
      compress: true,
      port: 3000,
    },
  };
  
  ```


### 配置路由模块

> 安装路由依赖
>
> 在src文件夹下创建路由文件夹routes
>
> 在routes文件夹下创建并配置index.jsx文件

`依赖安装`

```bash
npm i react-router-dom
```

`index.jsx配置`

```jsx
// 导入路由模块
import {BrowserRouter as Router,Routes,Route} from "react-router-dom";
// 导入路由组件
import Home from "../pages/Home";
import About from "../pages/About";

// 创建路由实例

const AppRoutes = () =>{
    return (
    	<Router>
        	<Routes>
            	<Route path="/" element={<Home />}/>
                <Route path="/about" element={<About />}/>
            </Routes>
        </Router>
    )
}

// 导出路由实例
export default AppRoutes;
```

`在入口文件中导入并使用路由`

```jsx
import AppRoutes from './routes';

ReactDOM.createRoot(document.getElementById('root').render(
<AppRoutes />
))
```



### 配置Redux模块

> 安装依赖
>
> 在src文件夹下创建store文件夹
>
> 在store文件夹下创建index.jsx配置redux store

`依赖安装`

```bash
npm i @reduxjs/toolkit react-redux
```

`配置redux`

```jsx
// 导入依赖
import {configureStore} from '@reduxjs/toolkit';
import counterReducer from './counterSlice';


// 创建store实例
export const store = configureStore({
    reducer:{
        counter: counterReducer,
    }
})
```

`创建counterSlice.js文件`

```js
// 导入模块
import {createSlice} from '@reduxjs/toolkit';

// 创建实例
export const counterSlice = createSlice({
    name: 'counter',
    initialState: {value:0},
    reducers:{
        increment:(state)=>{
            state.value +=1;
        },
        decrement: (state) =>{
            state.value -=1;
        }
    }
});
// 导出模块
export const { increment,decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

`在入口文件中导入并使用redux`

```jsx
import {Provider}from 'react-redux';
import {store} from './store';

ReactDOM.createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <AppRoutes />
  </Provider>
);

```

### 封装配置接口调用

> 接口调用的方式ajax、axios、fetch
>
> 使用axios调用
>
> 安装axios依赖
>
> 在src文件夹下创建api文件夹
>
> 在api文件夹下创建index.js用于封装接口请求

```js
// 导入axios依赖
import axios from 'axios';

// 创建axios实例
const instance = axios.create({
    baseURL: 'https://api.qingqiutoudizhi.com', // 设置请求头地址
    timeout: 10000, // 设置请求超时时间
})

// 设置请求拦截
instance.interceptors.request.use((config)=>{
    //在此处编写请求拦截逻辑
    return config;
})

// 设置响应拦截
instance.interceptors.response.use(
(response) => response, // 接口响应成功处理
(err)=>{
    // 接口响应错误处理
    return Promise.reject(error);
}
)

// 导出接口请求实例
export default instance;
```

### 封装常用工具类

> 在src目录下创建utils文件夹
>
> 在utils文件夹下创建工具类

`创建日期格式转换工具`

```js
// date.js
export const formaDate = (date) =>{
    const d = new Date(date);
    return `${d.getFullYear()}-${d.getMonth()+1}-${d.getDate()}`;
};
```

### 封装错误边界组件

> 在src目录下创建components文件夹
>
> 在components文件夹下创建ErrorBoundary.jsx组件
>
> 在错误边界组件中编写逻辑

```jsx
import React from 'react';

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // 更新状态，以便下次渲染可以显示降级UI
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // 你也可以将错误日志上报到服务器
    console.error("ErrorBoundary caught an error", error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // 你可以自定义降级UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}

export default ErrorBoundary;

```

### 配置环境变量

> 环境变量可以让你根据不同的环境（开发、测试、生产）使用不同的配置
>
> 安装插件
>
> 创建.env文件
>
> 配置webpack
>
> 

