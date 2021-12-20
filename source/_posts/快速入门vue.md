---
title: 快速入门vue
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
内联

```
<div :class="{active: isActive}"></div>

data: {
    isActive: true
}
```

对象

```
<div :class="classObject"></div>

data: {
    classObject: {
        active" true,
        'text-danger': false
    }
}
```

计算属性

```
<div :class="classObject"></div>

data: {
    isActive: true,
    error: null
}

computed: {
    classObject: function () {
        return {
            active: this.isActive && !this.error,
            'text-danger': this.error && this.error.type === 'fatal'
        }
    }
}

```

数组

```
<div v-bind:class="[activeClass, errorClass]"></div>

data: {
    activeClass: 'active',
    errorClass: 'text-danger'
}
```

三元表达式

```
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```
数组中使用对象
```
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```


11. 条件渲染
v-if指令用于条件性地渲染一块内容

```
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

总结：
    不建议v-if与v-for一起使用，v-for具有比v-if更高的优先级，


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
（1）组件命名
- 使用 kebab-case

```
Vue.component('my-component-name', { /* ... */ })

/*
当使用 kebab-case (短横线分隔命名) 定义一个组件时，你也必须在引用这个自定义元素时使用 kebab-case，例如 <my-component-name>
*/ 
```

- 使用 PascalCase

```
Vue.component('MyComponentName', { /* ... */ })

/*
当使用 PascalCase (首字母大写命名) 定义一个组件时，你在引用这个自定义元素时两种命名法都可以使用。也就是说 <my-component-name> 和 <MyComponentName> 都是可接受的
*/
```

（2）通过props向子组件传递数据
- Prop命名

```
Vue.component('blog-post', {
  // 在 JavaScript 中是 camelCase 的
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})

<!-- 在 HTML 中是 kebab-case 的 -->
<blog-post post-title="hello!"></blog-post>
```

- Prop类型
通常你希望每个 prop 都有指定的值类型，这时，你可以以对象形式列出 prop

```
props: ['title', 'likes', 'isPublished', 'commentIds', 'author']

props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // or any other constructor
}
```

- 传递静态或动态Prop
静态Prop

```
<blog-post title="My journey with Vue"></blog-post>
```

动态Prop

```
<!-- 动态赋予一个变量的值 -->
<blog-post v-bind:title="post.title"></blog-post>

<!-- 动态赋予一个复杂表达式的值 -->
<blog-post
  v-bind:title="post.title + ' by ' + post.author.name"
></blog-post>
```

传入数字

```
<!-- 即便 `42` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:likes="42"></blog-post
```

传入布尔值

```
<!-- 包含该 prop 没有值的情况在内，都意味着 `true`。-->
<blog-post is-published></blog-post>

<!-- 即便 `false` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:is-published="false"></blog-post>
```

传入数组

```
<!-- 即便数组是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:comment-ids="[234, 266, 273]"></blog-post>
```

传入对象

```
<!-- 即便对象是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post
  v-bind:author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }"
></blog-post>
```


- 单向数据流
所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外变更父级组件的状态，从而导致你的应用的数据流向难以理，你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告

- Prop验证
type类型：String、Number、Boolean、Array、Object、Date、Function、Symbol

```
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }
})
```

（2）通过$emit监听子组件事件

```
// 父组件
<blog-post
  ...
  v-on:enlarge-text="postFontSize += 0.1"
></blog-post>

// 子组件
<button v-on:click="$emit('enlarge-text')">
  Enlarge text
</button>
```

- $emit参数

```
// 父组件
<blog-post
  ...
  v-on:enlarge-text="onEnlargeText"
></blog-post>

methods: {
    onEnlargeText (enlargeAmount) {
        this.postFontSize += enlargeAmount
    }
}

// 子组件
<button v-on:click="$emit('enlarge-text', 0.1)">
  Enlarge text
</button>
```

（3）插槽slot
一套内容分发的 API

```
<navigation-link url="/profile">
  Your Profile
</navigation-link>

// navigation-link
<a
  v-bind:href="url"
  class="nav-link"
>
  <slot></slot>
</a>

// 父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。
```

- 具名插槽

```
// 定义插槽
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>

// 使用插槽
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
```

- 作用域插槽

```
// 子组件
<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>

// 父组件
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```


（4）动态组件
总结：
（1）组件的data必须一个函数

16. 自定义事件

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

钩子函数参数
el：指令所绑定的元素，可以用来直接操作 DOM
binding：一个对象，包含以下 property
    name：指令名，不包括 v- 前缀
    value：指令绑定的值，例如：v-my-directive="1 + 1" 中，绑定值为 2
    oldValue：指定绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用
    expression：字符串形式的指定表达式，例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"
    arg：传给指令的参数，例如 v-my-directive:foo 中，参数为 "foo"
    modifers：一个包含修饰符的对象，如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }
vnode：Vue 编译生成的虚拟节点
oldVnode：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用

一个例子

```
<div id="hook-arguments-example" v-demo:foo.a.b="message"></div>

Vue.directive('demo', {
  bind: function (el, binding, vnode) {
    var s = JSON.stringify
    el.innerHTML =
      'name: '       + s(binding.name) + '<br>' +   //demo
      'value: '      + s(binding.value) + '<br>' +  // hello
      'expression: ' + s(binding.expression) + '<br>' + // message
      'argument: '   + s(binding.arg) + '<br>' +    //foo
      'modifiers: '  + s(binding.modifiers) + '<br>' +  //{"a": true, "b": true}
      'vnode keys: ' + Object.keys(vnode).join(', ')
  }
})

new Vue({
  el: '#hook-arguments-example',
  data: {
    message: 'hello!'
  }
})
```


##### 20. Render & JSX
Vue 推荐在绝大多数情况下使用模板来创建你的 HTML。然而在一些场景中，你真的需要 JavaScript 的完全编程的能力。这时你可以用渲染函数，它比模板更接近编译器

```
Vue.component('anchored-heading', {
  render: function (createElement) {
    return createElement(
      'h' + this.level,   // 标签名称
      this.$slots.default // 子节点数组
    )
  },
  props: {
    level: {
      type: Number,
      required: true
    }
  }
})
```

- 节点、树以及虚拟 DOM

```
<h1>{{ blogTitle }}</h1>

渲染函数

render: function (createElement) {
  return createElement('h1', this.blogTitle)
}
```

- createElement 参数

```
// @returns {VNode}
createElement(
  // {String | Object | Function}
  // 一个 HTML 标签名、组件选项对象，或者
  // resolve 了上述任何一种的一个 async 函数。必填项。
  'div',

  // {Object}
  // 一个与模板中 attribute 对应的数据对象。可选。
  {
    // (详情见下一节)
  },

  // {String | Array}
  // 子级虚拟节点 (VNodes)，由 `createElement()` 构建而成，
  // 也可以使用字符串来生成“文本虚拟节点”。可选。
  [
    '先写一些文字',
    createElement('h1', '一则头条'),
    createElement(MyComponent, {
      props: {
        someProp: 'foobar'
      }
    })
  ]
)
```

##### 21. 插件
（1）插件是什么？
    插件通常用来为 Vue 添加全局功能
（2）怎么用？
    通过全局方法 Vue.use() 使用插件，它需要在你调用 new Vue() 启动应用之前完成

```
// 调用 `MyPlugin.install(Vue)`
Vue.use(MyPlugin)

new Vue({
  // ...组件选项
})
```

（3）开发插件
Vue.js 的插件应该暴露一个 install 方法。这个方法的第一个参数是 Vue 构造器，第二个参数是一个可选的选项对象：

```
MyPlugin.install = function (Vue, options) {
  // 1. 添加全局方法或 property
  Vue.myGlobalMethod = function () {
    // 逻辑...
  }

  // 2. 添加全局资源
  Vue.directive('my-directive', {
    bind (el, binding, vnode, oldVnode) {
      // 逻辑...
    }
    ...
  })

  // 3. 注入组件选项
  Vue.mixin({
    created: function () {
      // 逻辑...
    }
    ...
  })

  // 4. 添加实例方法
  Vue.prototype.$myMethod = function (methodOptions) {
    // 逻辑...
  }
}
```

##### 22. 过滤器
Vue.js 允许你自定义过滤器，可被用于一些常见的文本格式化

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

##### 23. 响应式原理
![vue](vue.png)
每个组件实例都对应一个 watcher 实例，它会在组件渲染的过程中把“接触”过的数据 property 记录为依赖。之后当依赖项的 setter 触发时，会通知 watcher，从而使它关联的组件重新渲染

##### 24. 测试
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

##### 25. Vue API
- 实例
（1）vm.$data
（2）vm.$props
（3）vm.$el
    Vue 实例使用的根 DOM 元素
（3）vm.$options
    用于当前 Vue 实例的初始化选项

```
new Vue({
  customOption: 'foo',
  created: function () {
    console.log(this.$options.customOption) // => 'foo'
  }
})
```

（4）vm.$parent
    父实例，如果当前实例有的话
（5）vm.$root
    当前组件树的根 Vue 实例。如果当前实例没有父实例，此实例将会是其自己
（6）$children
    当前实例的直接子组件
（7）vm.$slots
    用来访问被插槽分发的内容

    ```
    <blog-post>
        <template v-slot:header>
            <h1>About Me</h1>
        </template>

        <p>Here's some page content, which will be included in vm.$slots.default,   because it's not inside a named slot.
        </p>

        <template v-slot:footer>
            <p>Copyright 2016 Evan You</p>
        </template>

        <p>If I have some content down here, it will also be included in            vm.$slots.default.
        </p>
    </blog-post>
    ```

    ```
    Vue.component('blog-post', {
        render: function (createElement) {
            var header = this.$slots.header
            var body   = this.$slots.default
            var footer = this.$slots.footer
            return createElement('div', [
            createElement('header', header),
            createElement('main', body),
            createElement('footer', footer)
            ])
        }
     })
    ```
（8）vm.$scopedSlots
    用来访问作用域插槽。对于包括 默认 slot 在内的每一个插槽，该对象都包含一个返回相应 VNode 的函数。
（9）vm.$refs
    一个对象，持有注册过 ref attribute 的所有 DOM 元素和组件实例
（10）vm.$isServer
    当前 Vue 实例是否运行于服务器
（11）vm.$attrs
    包含了父作用域中不作为 prop 被识别 (且获取) 的 attribute 绑定 (class 和 style 除外)。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 (class 和 style 除外)，并且可以通过 v-bind="$attrs" 传入内部组件——在创建高级别的组件时非常有用
（12）vm.$listeners
    包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器。它可以通过 v-on="$listeners" 传入内部组件——在创建更高层次的组件时非常有用


- 实例方法
（1）vm.$watch( expOrFn, callback, [options] )
    观察 Vue 实例上的一个表达式或者一个函数计算结果的变化。回调函数得到的参数为新值和旧值。表达式只接受简单的键路径。对于更复杂的表达式，用一个函数取代
    ```
        // 键路径
        vm.$watch('a.b.c', function (newVal, oldVal) {
        // 做点什么
        })

        // 函数
        vm.$watch(
        function () {
            // 表达式 `this.a + this.b` 每次得出一个不同的结果时
            // 处理函数都会被调用。
            // 这就像监听一个未被定义的计算属性
            return this.a + this.b
        },
        function (newVal, oldVal) {
            // 做点什么
        }
        )
    ```

    vm.$watch 返回一个取消观察函数，用来停止触发回调：

    ```
    var unwatch = vm.$watch('a', cb)
    // 之后取消观察
    unwatch()
    ```

    选项：deep
        为了发现对象内部值的变化，可以在选项参数中指定 deep: true。注意监听数组的变更不需要这么做。
    ```
        vm.$watch('someObject', callback, {
            deep: true
        })
        vm.someObject.nestedValue = 123
        // callback is fired
    ```


    选项：immediate
        在选项参数中指定 immediate: true 将立即以表达式的当前值触发回调：

    ```
        vm.$watch('a', callback, {
            immediate: true
        })
        // 立即以 `a` 的当前值触发回调
    ```


（2）vm.$set( target, propertyName/index, value )
    这是全局 Vue.set 的别名

（3）vm.$delete( target, propertyName/index )
    这是全局 Vue.delete 的别名

（4）vm.$on( event, callback )
    监听当前实例上的自定义事件。事件可以由 vm.$emit 触发。回调函数会接收所有传入事件触发函数的额外参数

    ```
    vm.$on('test', function (msg) {
        console.log(msg)
    })
    vm.$emit('test', 'hi')
    // => "hi"
    ```

（5）$once
    监听一个自定义事件，但是只触发一次。一旦触发之后，监听器就会被移除
（6）vm.$off( [event, callback] )
    移除自定义事件监听器
    - 如果没有提供参数，则移除所有的事件监听器；

    - 如果只提供了事件，则移除该事件所有的监听器；

    - 如果同时提供了事件与回调，则只移除这个回调的监听器。

（7）vm.$emit( eventName, […args] )
    触发当前实例上的事件。附加参数都会传给监听器回调
    ```
    Vue.component('welcome-button', {
        template: `
            <button v-on:click="$emit('welcome')">
                Click me to be welcomed
            </button>`
    })
    ```

    ```
    <div id="emit-example-simple">
        <welcome-button @welcome="sayHi"></welcome-button>
    </div>
    ```

    ```
    new Vue({
        el: '#emit-example-simple',
        methods: {
            sayHi: function () {
            alert('Hi!')
            }
        }
    })
    ```
（8）vm.$mount( [elementOrSelector] )
    如果 Vue 实例在实例化时没有收到 el 选项，则它处于“未挂载”状态，没有关联的 DOM 元素可以使用 vm.$mount() 手动地挂载一个未挂载的实例

（9）vm.$nextTick( [callback] )
    将回调延迟到下次 DOM 更新循环之后执行。在修改数据之后立即使用它，然后等待 DOM 更新。它跟全局方法 Vue.nextTick 一样，不同的是回调的 this 自动绑定到调用它的实例上

（10）vm.$destroy()
     完全销毁一个实例。清理它与其它实例的连接，解绑它的全部指令及事件监听器  

（11）vm.$forceUpdate()
    迫使 Vue 实例重新渲染。注意它仅仅影响实例本身和插入插槽内容的子组件，而不是所有子组件

