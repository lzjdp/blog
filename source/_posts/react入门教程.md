---
title: react入门教程
date: 2021-10-31 21:22:53
tags:
---
1. JSX
react提供的语法糖，可以在js文件中插入html片段
（1）jsx中的class应该写成className
```
<input className="username" />
```

（2）注释
```
{/* 注释内容 */}
```

2. 组件
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

4. state


5. props

6. refs

7. 事件处理

8. 条件渲染

9. 列表

10. 高阶组件

11. 状态提升

12. 表单

13. context

