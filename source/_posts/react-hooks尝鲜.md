---
title: react-hooks尝鲜
date: 2019-04-24 18:14:09
tags: [前端, JS, React, react-hooks]
categories:
- 前端
- React
---

## what is a Hooks?

Hooks是指函数组件“hook into”反应状态和生命周期特性的函数。Hooks在类中不起作用，它可以在没有类的情况下直接使用React。（不建议重写现有组件，可以在新的组件中使用Hooks）

<!-- more -->

## 钩子一瞥

> 钩子是在React 16.8中新增的。它们允许您在不编写类的情况下使用状态和其他反应特性。

1. State Hook

> 🌰 点击按钮自增数

- 之前的写法
```
  import React, { Component } from 'react'

  class App extends Component {
    constructor(props) {
      super(props)
      this.state = {
        count: 0
      }
    }
    render() {
      const {
        count
      } = this.state;
      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => this.setState({ count: count + 1 })}>
            Click me
          </button>
        </div>
      );
    }
  }

  export default App;
```
- 用了 hooks 的写法
```
  import React, { useState } from 'react'

  function App() {
    const [count, setCount] = useState(0)
    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
          Click me
        </button>
      </div>
    );
  }

  export default App
```

  * `useState` 是一个钩子，我们在一个函数组件内部调用它来向它添加一些本地的状态
  * react将在重新渲染之间保留这个状态
  * `useState` 返回一对数据：当前状态值和一个允许更新它的函数，可以从时间处理或者其他地方调用这个返回函数，类似 ~~this.setState~~，不同的是它不将新旧状态合并在一起
  * 还有一点需要注意, `useState` 的唯一参数是初始状态，在上面的栗子中，它的初始状态是0。与 ~~this.state~~ 不同：这里的状态不一定是一个对象；且初始状态参数仅在第一次期间使用

> 🌰 声明多个状态变量

```
  function ExampleWithManyStates() {
    // Declare multiple state variables!
    const [age, setAge] = useState(42);
    const [fruit, setFruit] = useState('banana');
    const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
    // ...
  }
```

> React 提供类一些内置的钩子，比如刚才使用的 `useState` ，也可以自己创建钩子来重用不同组件之间的状态行为。

2. Effect Hook

Effect Hook，它与componentDidMount、componentDidUpdate和componentWillUnmount的作用相同

> 栗子 更新DOM后设置文档标题

- 之前的写法

```
  import React, { Component } from 'react'

  class App extends Component {
    constructor(props) {
      super(props)
      this.state = {
        count: 0
      }
    }
    componentDidMount() {
      const {
        count
      } = this.state
      document.title = `You clicked ${count} times`
    }
    componentDidUpdate() {
      const {
        count
      } = this.state
      document.title = `You clicked ${count} times`
    }
    render() {
      const {
        count
      } = this.state;
      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => this.setState({ count: count + 1 })}>
            Click me
          </button>
        </div>
      );
    }
  }

  export default App;
```

- 使用了 Hooks

```
  import React, { useState, useEffect } from 'react';

  function Example() {
    const [count, setCount] = useState(0);

    // Similar to componentDidMount and componentDidUpdate:
    useEffect(() => {
      // Update the document title using the browser API
      document.title = `You clicked ${count} times`;
    });

    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
          Click me
        </button>
      </div>
    );
  }
```

  * 默认情况下，React 会在每次渲染后调用副作用函数（包括第一次渲染）
  * 副作用函数还可以通过返回一个函数来指定如何“清除”副作用。它的执行顺序是，每次页面更新前，先执行 return 函数，然后再执行 `useEffect` 里的内容
  * 跟 `useState` 一样，可以在组件中多次使用 `useEffect` ，通过使用 Hooks，你可以把组件内相关的副作用函数组织在一起，（比如创建订阅和取消订阅），这样的好处在于不用把它们拆分在不同的生命周期函数里面
  * `useEffect` 还可以传入第二个参数，指定某个值发生变化的时候才触发

```
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count])
```
  * 如果只想运行一次 `useEffect`，可以把第二个参数改为一个空数组

3. ⚠️ Rules of Hooks

Hooks 是属于 JavaScript 函数，但是他们还附加了两条规则

- 只有顶层才能使用 Hooks， 不要在循环、条件、或者嵌套函数内调用挂钩
- 只有在 React 函数组件中调用挂钩，不要从常规的 JavaScript 函数调用钩子。（只有一个有效地方可以调用钩子 - 自定义钩子）

4. 自定义钩子

很多时候我们的组件都会存在状态逻辑的重用，在传统上，我们会用到两种比较流行的解决方案：
- 高阶组件
- 渲染道具
但是现在出现了 Hooks，我们可以自定义一些钩子函数，且它不会向树中添加更多的组件

首先，我们自定义一个重用的函数钩子

```
  import React, { useState, useEffect } from 'react';

  function useFriendStatus(friendID) {
    const [isOnline, setIsOnline] = useState(null);

    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    useEffect(() => {
      ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
      return () => {
        ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
      };
    });

    return isOnline;
  }
```
以 `friendID` 作为参数，放回我们的朋友是否在线

然后其他组件可以这样使用它：

- 🌰 1

```
  function FriendStatus(props) {
    const isOnline = useFriendStatus(props.friend.id);

    if (isOnline === null) {
      return 'Loading...';
    }
    return isOnline ? 'Online' : 'Offline';
  }
```

- 🌰 2

```
  function FriendListItem(props) {
    const isOnline = useFriendStatus(props.friend.id);

    return (
      <li style={{ color: isOnline ? 'green' : 'black' }}>
        {props.friend.name}
      </li>
    );
  }
```

  * 这些组件的状态完全独立
  * 钩子是一种重用有状态逻辑的方法，而不是状态本身
  * 每个调用钩子的函数都是完全独立的状态，所以可以在一个组件中使用同一个自定义钩子两次
  * 自定义的钩子函数注意：需要以“use”开头并调用其他的钩子useSomething，这样方便linter插件如何使用钩子在代码中查找错误

5. 其他钩子

- useContext

> 接收一个 context 对象（React.createContext 的返回值）并返回该 context 的当前值。当前的 context 值由上层组件中距离当前组件最近的 <MyContext.Provider> 的 value prop 决定

- useReducer

> useState 的替代方案。它接收一个形如 (state, action) => newState 的 reducer，并返回当前的 state 以及与其配套的 dispatch 方法。（如果你熟悉 Redux 的话，就已经知道它如何工作了。）

- 🌰 reducer.js
```
  const initialState = {count: 0};

  function reducer(state, action) {
    switch (action.type) {
      case 'increment':
        return {count: state.count + 1};
      case 'decrement':
        return {count: state.count - 1};
      default:
        throw new Error();
    }
  }

  function Counter({initialState}) {
    const [state, dispatch] = useReducer(reducer, initialState);
    return (
      <>
        Count: {state.count}
        <button onClick={() => dispatch({type: 'increment'})}>+</button>
        <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      </>
    );
  }
```

完整 demo [请点击我](https://github.com/MrMeiyu/webpack4.0-react/tree/react-hooks)

使用以前最好看下 [官方文档](https://reactjs.org/docs/hooks-intro.html)
因为中文React文档还没有更新到最新的版本，所以我也是看的英文的文档
