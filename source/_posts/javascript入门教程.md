---
title: javascript入门教程
date: 2020-1-30 23:13:02
tags:
---

##### 1. 关于javascript
    JavaScript 是互联网上最流行的脚本语言

##### 2. 历史版本
    1997    ECMAScript1
    1998    ECMAScript2
    1999    ECMAScript3
    2009    ECMAScript5
    2011    ECMAScript5.1
    2015    ECMAScript6
    2016    ECMAScript7

##### 3. 数据类型
   值类型（基本类型）：字符串（String）、数字(Number)、布尔(Boolean)、对空（Null）、未定义（Undefined）、Symbol

   引用数据类型：对象(Object)、数组(Array)、函数(Function) 

   null表示一个空对象引用
   undefined表示未定义、未初始化
```
// null与undefined值相等，但类型不等
null === undefined   // false
null == undefined   // true
```

##### 4. 条件语句
    if 
    if...else
    if...else...if
    switch  
```
switch (n) {
    case 1:
        执行代码块 1
        break;
    case 2:
        执行代码块 2
        break;
    default: 
        与 case 1 和 case 2 不同时执行的代码
}
``` 
    

5. 循环语句
for
for/in
while
do/while

```
for (语句 1; 语句 2; 语句 3) {
    被执行的代码块
}

var person={fname:"Bill",lname:"Gates",age:56}; 
 
for (x in person)  // x 为属性名
{
    txt=txt + person[x];
}

while (条件)
{
    需要执行的代码
}

do
{
    需要执行的代码
}
while (条件)
```

##### 6. typeof
作用：判断变量数据类型，可判断string、number、boolean、undefined、function、object
```
typeof 'abc'    // string
typeof 12   // number
typeof true // boolean
typeof null // object
typeof function fn(a, b) => {return a + b}  // function
typeof [1,2,3]  // object
```

##### 7. 正则表达式
   正则表达式是由一个字符序列形成的搜索模式

##### 8. 变量提升
JavaScript 中，函数及变量的声明都将被提升到函数的最顶部，变量可以在使用后声明
```
x = 5; // 变量 x 设置为 5

elem = document.getElementById("demo"); // 查找元素
elem.innerHTML = x;                     // 在元素中显示 x

var x; // 声明 x
```

##### 9. this关键字
    面向对象语言中 this 表示当前对象的一个引用
（1）在方法中，this 表示该方法所属的对象。
（2）如果单独使用，this 表示全局对象。
（3）在函数中，this 表示全局对象。
（4）在函数中，在严格模式下，this 是未定义的(undefined)。
（5）在事件中，this 表示接收事件的元素。
（6）类似 call() 和 apply() 方法可以将 this 引用到任何对象。
```
// 单独使用this，指向全局对象
var x = this
console.log(this)   // Window

// 对象方法中使用this，指向它所在方法的对象
var person = {
    name: 'carr',
    showName: function () {
        console.log(this.name)  // carr
    }
}

// 函数中使用this，严格模式下指向undefined，非严格模式下指向全局对象
function fn () {
    console.log(this)   // Window
}
function fn () {
    'use strict';
    console.log(this)
}

// 事件中的this，指向接受事件的HTML元素
<button onClick="this.style.display='none'"></button>

// 使用call改变this指向
var person1 = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
var person2 = {
  firstName:"John",
  lastName: "Doe",
}
person1.fullName.call(person2);  // 返回 "John Doe"
``` 

##### 10. 函数
（1）函数声明
```
function fn (a, b) { return a + b }
```

(2) 函数表达式
```
var fn = function (a, b) { return a + b }
```

(3) 函数提升
函数可以在声明之前调用
```
fn()
function fn (a, b) {
    return a + b
}
```

(4) 自执行函数
```
(function())(
    console.log('hello')
)
```

(5) 函数是对象
函数有arguments属性，它是包含所有参数的数组
```
function fn (a, b) {
    return arguments.length
}
```

(6) 箭头函数
箭头函数没有自己的this，箭头函数中的this和外层this的值一样
箭头函数没有arguments属性
箭头函数不能作为构造函数

(7) 默认参数
```
// ES5设置默认参数
function fn (x, y) {
    y = y || 0
}

// ES6设置默认参数
function fn (a, b = 0) {
    return a + b
}
```

(8) 闭包
```
var add = (function () {
    var counter = 0
    return function () {
        return counter += 1
    }
})()
```

##### 13. 面向对象
(1)原型

(2)原型链

(3)继承

##### 14. String
(1) indexOf // 返回字符串中某一个指定的字符首次出现的位置
```
var str = 'Hello world, wclcome to the universe'
var n = str.indexOf('welcome')
```

(2) match

(3) replace()

(4) toUpperCase() / toLowerCase()

(5) split()

(6) slice()

(7) search()

(8) substr()

(9) valueOf()

(10) charAt()

(11) charCodeAt()

##### 15. Number

##### 16. Array

##### 17. Boolean

##### 18. Math

##### 19. Date

##### 20. RegExp

##### 21. DOM
(1) DOM(Document object Model) 文档对象模型
(2) DOM事件
onload/onunload 进入或离开页面时触发
onchange
onmouseover
onmouseout
onmousedown
onmouseup
onclik

(3) 事件绑定
addEventListener    // 事件绑定
removeEventListener // 解除事件绑定

```
element.addEventListener('click', function () {
    console.log('hello world')
})
```

(4)事件冒泡和事件捕获
事件传递的方式有两种：事件冒泡或事件捕获
在冒泡中，内部元素的事件会先触发。然后再触发外部元素
在捕获中，外部元素的事件会被先触发，然后才会触发内部元素

(5)向Window对象添加事件
```
window.addEvenetListener('resize', function () {
    ...
})
```

##### 22. BOM
(1) BOM(Browser object Model) 浏览器对象模型 

(2) window尺寸
window.innerHeight  浏览器窗口的内部高度(包括滚动条)
window.innerWidth - 浏览器窗口的内部宽度(包括滚动条)

(3)window方法
window.open()   打开新窗口
window.close()  关闭当前窗口
window.moveTo() 移动当前窗口
window.resizeTo()  调整当前窗口的尺寸

(4)