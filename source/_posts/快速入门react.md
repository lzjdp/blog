---
title: 快速入门react
date: 2021-10-31 21:22:53
tags:
---
1. React是什么？
React 是一个声明式，高效且灵活的用于构建用户界面的 JavaScript 库

2. JSX
react提供的语法糖，可以在js文件中插入html片段
（1）jsx中的class应该写成className
```
<input className="username" />
```

（2）注释
```
{/* 注释内容 */}
```

3. 组件和props
（1）类组件
```
import React from 'react'
class MyComponent extends Ract.Component {
    render () {
        return {
            <div>Hello React</div>
        }
    }
}
```

（2）函数组件
```
function MyComponent () {
    return <div>Hello React</div>
}
```

（3）组件状态
```
import React from 'react'
class MyComponent extends React.Component {
    this.state = {
        num: 0
    }
    render () {
        return {
            <p>{this.state.num}</p>
        }
    }
}
```

3. 生命周期
componentDidMount   在组件已经被渲染到 DOM 中后运行
componentWillUnmount

4. state
```
class Clock extends React.Component {
    constructor (props) {
        super(props)
        this.state = {date: new Date()}
    }
    componentDidMount () {
        this.timerID = setInterval(() => {
            this.tick()
        },1000)
    }
    componentWillUnmount () {
        clearInterval(this.timerID)
    }
    tick () {
        this.setState({
            date: new Date()
        })
    }
    render () {
        return {
            <div>
                <h2>{this.state.date}</h2>
            </div>
        }
    }
}
```
总结：
1）不要直接修改State
2) State的更新可能是异步的
3）State的更新会被合并

5. 事件处理
```
class Toggle extends React.Component {
    constructor (props) {
        super(props)
        this.state = {isToggleOn: true}
        // 为了在回调中使用 `this`，这个绑定是必不可少的
        this.handlerClick = this.handleClick.bind(this)
    }
    handlerClick () {
        this.setState(state => {
            isToggleOn: !state.isToggleOn
        })
    }
    render () {
        return {
            <button onClick={}></button>
        }
    }
}
```
在 JavaScript 中，class 的方法默认不会绑定 this。如果你忘记绑定 this.handleClick 并把它传入了 onClick，当你调用这个函数的时候 this 的值为 undefined

解决this绑定问题的两种方法：
方法一：
```
class LoginButton extends React.Component {
    // 此语法确保 `handleClick` 内的 `this` 已被绑定。
    // 注意: 这是 *实验性* 语法。
    handlerClick = () => {
        console.log(this)
    }
    render () {
        return {
            <button onClick={this.handlerClick}>
                {this.state.isToggleOn ? 'ON' : 'OFF'}
            </button>
        }
    }
}
```
方法二：
```
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // 此语法确保 `handleClick` 内的 `this` 已被绑定。
    return (
      <button onClick={() => this.handleClick()}>
        Click me
      </button>
    );
  }
}
```

向事件处理程序传递参数
```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

注意事项：
1）React 事件的命名采用小驼峰式（camelCase），而不是纯小写
2）使用 JSX 语法时你需要传入一个函数作为事件处理函数，而不是一个字符串

8. 条件渲染

9. 列表

10. 高阶组件

11. 状态提升

12. 表单

13. context

