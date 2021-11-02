---
title: vue入门教程
date: 2021-10-31 21:19:30
tags:
---

1. vue简介
    Vue是一套用于构建用户界面的渐进式框架，Vue能够为复杂的单页面应用提供驱动

2. 安装
（1）CDN引入
```
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
```

（2）脚手架工具vue-cli
```
// 全局安装vue-cli
npm install vue-cli -g

// create vue project
vue init wepack demo-name   // for vue-cli@2.x

or

vue create  // for vue-cli@3.x
```

3. Vue实例
```
var data = {a: 1}
var vm = new Vue({
    data: data
})
```

4. 生命周期
![vue生命周期](lifecycle.png)

5. 插值（Mustache）
数据绑定最常见的形式就是使用'Mustache'语法（双大括号）的文本插值
```
<span>{{Message: {{msg}}}}</span>
```

6. 指令
指定（Directives）是带有v-前缀的特殊attribute，指令的指责是，当表达式的值改变时，
将其产生的连带影响，响应式的用于DOM
v-on    // 缩写 :
v-bind  // 缩写 @
v-if
v-else
v-else-if
v-html
v-for
v-show

7. 修饰符
.prevent

8. 计算属性(computed)
计算属性
```
var vm = new Vue({
    el: '#app',
    data: {
        message: 'Hello'
    },
    computed: {
        reversedMessage: function () {
            // this指向vm实例
            return this.message.split('').reverse().join('')
        }
    }
})
```

9. 侦听器
```
<div id="app">
    <p>
        Ask a yes/no question
        <input v-model="question" />
    </p>
</div>

var vm = new Vue({
    el: '#app',
    data () {
        return {
            question: '',
            answer: 'I cannot give you an answer until you ask a question!'
        }
    },
    created () {
        this.debouncedGetAnswer = _.debounce(this.getAnswer, 500)
    },
    watch: {
        question: function (newQuestion, oldQuestion) {
            this.answer = 'Waiting for you to stop typing...'
            this.debouncedGetAnswer()
        }
    },
    methods: {
        getAnsswer: function () {
            if (this.question.indexOf('?') === -1) {
                this.answer = ''Questions usually contain a question mark. ;-)'
                return 
            }
            this.answer = 'Thinking...'
            var vm = this
            axios.get('').then(res => {
                vm.answer = _.capitalize(response.data.answer)
            }).catch(error => {
                vm.answer = 'Error! Could not reach the API. ' + error
            })
        }
    }
})
```

10. class与style绑定
```

```

11. 条件渲染

12. 列表渲染
```
<ul>
    <li v-for="item in items" :key="item.message">
        {{item.message}}
    </li>
</ul>
```

总结：
（1）建议给每个遍历项添加一个唯一的key，且不是下标
（2）不建议v-for, v-if在上同一个元素上同时使用
（3）v-for的优先级高于v-if

13. 事件处理（v-on）
用v-on指令监听DOM事件
```
<div id="app">
    <button v-on:click="greet">Greet</button>
</div>

var app = new Vue({
    el: '#app',
    data: {
        name: 'Vue.js'
    },
    methods: {
        greet: function (event) {
            if (event) {
                alert(event.target.tagName)
            }
        }
    }
})
```
事件修饰符：
.stop
.prevent
.capture
.self
.once
.passive
.enter
.tab
.delete
.esc
.space
.up
.down
.left
.right
```
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

14. 表单输入绑定（v-model）
v-model
```
// 文本
<input v-model="message" />
<p>Message is: {{message}}</p>

// 复选框
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
```

修饰符：
.lazy   在“change”时而非“input”时更新
.trim   自动过滤用户输入的首尾空白字符
.number 将用户的输入值转为数值类型
```
<input v-model.lazy="msg">

<input v-model.number="age" type="number">

<input v-model.trim="msg">
```

15. 组件
（1）通过props向子组件传递数据
```
Vue.component('', {
    props: ['title'],
    temlate: '<h3>{{title}}</h3>'
})
```

（2）通过$emit监听子组件事件
```

```

（3）插槽slot
```

```

（4）动态组件
总结：
（1）组件的data必须一个函数

16. prop
(1)prop类型
Srtring
Number
Boolean
Array
Object
Function
Promise

(2) 单向数据流
所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外变更父级组件的状态，从而导致你的应用的数据流向难以理解

(3) prop验证

17. 进入离开列表过渡

18. 混入
```
var myMixin = {
    created: function () {
        this.hello()
    },
    methods: {
        hello: function () {
            console.log('hello')
        }
    }
}

var Component = Vue.extend({
    mixins: [myMixin]
})
```

19. 自定义指令
```
Vue.directive('focus', {
    // / 当被绑定的元素插入到 DOM 中时……
    inserted: function (el) {
        // 聚焦元素
    el.focus()
        el.focus()
    }
})
```
钩子函数：
bind    只调用一次，指令第一次绑定到元素时调用
inserted    被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)
update  所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前
componentUpdated    指令所在组件的 VNode 及其子 VNode 全部更新后调用
unbind  只调用一次，指令与元素解绑时调用

20. Render & JSX

21. 插件
通过全局方法 Vue.use() 使用插件
```
// 调用 `MyPlugin.install(Vue)`
Vue.use(MyPlugin)

new Vue({
  // ...组件选项
})
```
开发插件
```

```

22. 过滤器
```
<!-- 在双花括号中 -->
{{ message | capitalize}}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="rawId | formatId"></div>

filters: {
    capitalize: function (value) {
        if (!value) {
            value = value.toString()
            return value.chartAt(0).toUpperCase() + value.slice(1)
        }
    }
}
```
全局注册过滤器
Vue.filter('capitalize', function (value) {
    if (!value) {
        value = value.toString()
        return value.chartAt(0).toUpperCase() + value.slice(1)
    }
})

23. 插槽
```
<navigation-link url="/profile">
  Your Profile
</navigation-link>

<a
  v-bind:href="url"
  class="nav-link"
>
  <slot></slot>
</a>
```
具名插槽
```
<div class="container">
    <header>
        <slot name="header"></slot>
    </header>
    <main></main>
    <footer>
        <slot name="footer"></slot>
    </footer>
</div>

<base-layout>
    <template v-slot:header>
        <h1>Here might be a page title</h1>
    </template>
        <p>A paragraph for the main content.</p>
        <p>And another one.</p>
    <template v-slot:footer>
        <p>Here's some contact info</p>
    </template>
</base-layout>

// 任何没有被包裹在带有 v-slot 的 <template> 中的内容都会被视为默认插槽的内容
```

作用域插槽

24. 测试
（1）官方推荐测试框架Vue Testing Library (@testing-library/vue)

（2）安装
```
npm install --save-dev jest @vue/test-utils
```

（3）添加脚本
```
// package.json
{
  "scripts": {
    "test": "jest"
  }
}
```

（4）
