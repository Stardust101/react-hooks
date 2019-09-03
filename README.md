# react-hooks
## react-hooks初体验
最近在使用react-hooks开发项目，发现了一些有趣的地方，总结并分享出来。本篇是科普文，旨在说明react-hooks的用法，与之前使用react进行开发的一些比较，以及在使用react-hooks开发项目过程中的一些个人思考！!

## 举例说明hooks的特性

### Hooks是什么？
Hooks简单来说就是一个函数，使用函数的方式调用组件，全局不用使用this，不使用用react生命周期，所有的状态通过传参的方式进行全局的调用，开发者只关注状态的更新和传递，不用了解this，不用考虑使用哪个生命周期，比较简洁，下面通过两个小例子对hooks的基本使用进行分析。

### 使用Class的示例

```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}

```

### 使用hooks的示例

```
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  }, [count]);

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
### 比较hooks写法和class写法的区别

#### 关于this

0. this
    1. 在 class 中，无论是状态的使用，还是方法的调用，包括组件之间的参数传递，都需要绑定this，通过this的指向来展示数据的流动。
    1. 在hooks的组件中不需要this，全局都是函数式的调用方法，所有状态和方法都可以作为函数的参数进行传递，开发者不需要理解this指向了哪里，只需关注自己的方法调用即可。

#### 关于生命周期
0. 生命周期
    1. 在 class 中，状态和方法的更新需要考虑组件的生命周期。
    1. 在hooks的组件中不需要生命周期，方法调用即使用。

#### 关于状态的使用

0. 状态声明方式的差异
    1. 在 class 中，我们通过在构造函数constructor中设置 this.state 为 { count: 0 } 来初始化 count 为 0.
    1. 在hooks的组件中全局都不需要this，直接调用useState方法, useState(0), 来声明count 为0.

1. 更新状态的差异
    1. 在 class 中，我们通过调用this.setState({ count : 0})方法，来更新count的值.
    1. 在hooks中，同样直接调用useState的第二个参数, setCount(0), 来更新count的值为0.

2. 使用状态的差异
    1. 在 class 中，我们在组件中通过调用this.state.count方法，来使用count的值.
    1. 在hooks中，同样直接使用 count 即可.

#### 关于组件更新

0.  组价更新
    1. 在 class 中，我们希望在组件加载和更新时执行同样的操作，所以我们一般需要在componentDidMount的时候更新数据，有时候还需要在componentDidUpate的时候更新数据，同样的更新数据逻辑我们需要写两遍。
    1. 在hooks中，我们使用useEffect进行更新数据，只需要写一次，默认情况下，它在第一次渲染之后和每次更新之后都会执行.

0.  性能优化
    1. 如果频繁的调用生命周期函数可能会出现性能问题，在 class 中，我们可以通过shouldComponentDidUpdate来决定是否更新组件，也可以在 componentDidUpdate 中添加对 prevProps 或 prevState 的比较逻辑解决.
    1. 在hooks中，如果某些特定值在两次重渲染之间没有发生变化，我们可以通知React跳过对useEffect的调用，只要传递数组作为useEffect的第二个可选参数即可，比如上述的例子组件仅在count更改时才会进行重新渲染.


#### 未完待续



