---
title: vue面试题
date: 2021-10-29 13:56:59
tags:
---

##### 1.vue2.0生命周期有哪些？
```
beforeCreate    组件创建，元素dom和数据还没有初始化
created         数据data已经初始化完成，方法可以调用，但dom未渲染
beforeMount     dom未挂载，数据初始化已完成，但双向绑定还是显示{{}}
mounted         dom完成挂载，一般数据请求放在这里，因为请求改变数据之后刚好渲染
beforeUpdate    页面数据改变了都会触发
updated         只要页面数据改变了都会触发，页面更新完毕
beforeDestory   组件销毁之前执行
destoryed       组件销毁
```

##### 2.v-model的实现原理？
v-model在表单input、textarea、select等元素上创建双向数据绑定，v-model本质上是语法糖

##### 3.vue响应式原理？
数据劫持+观察者模式
使用Object.defineProperty将属性进行劫持，数组则是通过重写数据来实现，当页面使用对应属性时，
每个属性都拥有自己的dep属性，存在它所依赖的watcher(依赖收集)get，当属性变化后通知自己对应的watcher去更新(派发更新)set

##### 4.$nextTick有什么作用？
修改data的值后，需要立即获取dom元素的值，是获取不到的，因为vue是异步渲染的，
需要通过$nextTick获取

##### 5.v-if与v-show的区别？
共同点：都能控制元素的显示和隐藏
不同点：v-show的本质是利用display:none/block来控制元素的显示和隐藏
       v-if是动态的向dom树添加或删除元素，v-if创建和删除相比v-show更消耗性能
使用建议：如果需要频繁的切换元素建议使用v-show    

##### 6.computed计算属性与methods的区别？
computed计算属性有缓存的的功能，只有当指定数据变时，计算属性才会执行，否则否好原来的数据
methods没有缓存功能，每次渲染都会执行

##### 7.keep-alive的作用？
keep-alive用来对组件进行缓存

##### 8.组件通信的方法？
1. props和$emit 父子组件通信
2. $parent和$children  获取
3. $attrs和$liteners A->B->C
4. provide inject注入变量
5. $refs获取组件实例
6. EventBus兄弟组件传递数据
7. vuex状态管理
```
// 父组件
<template>
    <child :name="childName" :changeCount="getCount" />
</template>
<script>
import Child from './Child'
export default {
    components: {
        Child
    },
    data () {
        return {
            childName: 'carr'
        }
    },
    getCount (count) {
        console.log(count)
    }
}
</script>

// 子组件
<template>
    <div>
        <p>{{myName}}</p>
        <button @click="changeName">{{count}}</button>
    </div>
</template>
<script>
export default {
    // 父向子用props
    props: {
        myName: {
            type: String,
            default: ''
        }
    },
    data () {
        return {
            count: 0
        }
    },
    methods: {
        changeName () {
            this.count += 1
            this.$emit('changeCount', this.count)
        }
    }
}
</script>
```


##### 9.什么是MVVM?
M: 模型层
VM: 视图模型
V: 视图层
VM通过数据绑定将后端传递的数据转化成页面，通过DOM事件监听的方式将页面转换为数据传给后端

##### 10.遍历为什么要使用key？
key是为Vue中Vnode的唯一标识，通过这个key，我们的diff操作可以更准确、更快速

##### 11.vue中的data为什么要是一个函数？
组件的data写成一个函数，数据以函数返回值的形式定过，这样每复用一次组件，就会返回一份新的data，
类似于给每个组件实例创建一个私有的数据空间，让每个组件实例维护各自的数据，单纯写成对象的形式，
就使得所有组件实例共享一份data

##### 12.v-if和v-for的优先级？
v-for的优先级高于v-for

##### 13.怎样理解vue单向数据流？
数据总是从父组件传到子组件，子组件没有权利修改父组件传过来的数据，只能请求父组件对原始数据进行
修改，这样会防止子组件意外改变父组件的状态，从而导致你的应用数据流向难以理解

##### 14.computed和watch的区别及应用场景？
computed是计算属性，依赖其它属性计算值，且computed的值有缓存
watch监听到值的变化会执行回调，在回调中可以进行一系列操作
计算属性一般用载模板渲染中，某个值时依赖其它属性计算而来，watch适用于观测某个值的变化去完成
一些复杂的业务逻辑

##### 15.vue如何监测数组变化？
基于性能原因，没有用defineProperty对数组每一项进行拦截，二十选择对7种数组方法进行重写
push shift  pop splice  unshift sort  reverse

##### 16.vue3有哪些变化？
1. 响应式原理改变，vue3使用Proxy取代vue2版本的Object.defineProperty
2. 新增了Composition API

##### 17.虚拟DOM时什么？
在浏览器中操作DOM是很昂贵的，频繁操作DOM，会产生一定的性能问题，虚拟DOM本质时用一个原生的JS对象
去描述一个DOM节点，时对真实DOM的一层抽象

##### 18.vue事件绑定原理？

##### 19.vue父子组件生命周期钩子函数执行顺序
Vue 的父组件和子组件生命周期钩子函数执行顺序可以归类为以下 4 部分：

加载渲染过程

父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted

子组件更新过程

父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated

父组件更新过程

父 beforeUpdate -> 父 updated

销毁过程

父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed

##### 20.动态绑定class和style
```
// 对象语法
<div :class="{'active': isActive, 'text-danger': hasError}"></div>

// 数组语法
<div :class="[isActive ? 'activeClass' : '', 'errorClass']"></div>

// 对象语法
<div :style="{color: activeColor, fontSize: fontSize + 'px'}"></div>

// 数组语法
<div :style="[styleColor, styleSize]"></div>
```
