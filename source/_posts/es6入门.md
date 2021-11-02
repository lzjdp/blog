---
title: es6入门
date: 2021-10-29 14:25:17
tags:
---

##### 1. let const
(1) let用于定义变量，const用于定义常量
(2) let、const存在块级作用域
(3) let不与许在同作用域内重复声明
(4) const一旦声明不可改变
(5) const声明不可重复
(6) 不存在变量提升，必须先声明再使用

##### 2. 解构赋值
（1）数组解构赋值
```
let [a, b, c] = [1, 2, 3]
let [x, , y] = [1, 2, 3]
let [head, ...tail] = [1, 2, 3, 4]
```

（2）对象解构赋值
```
let {foo, bar} = { foo: 'aaa', bar: 'bbb' }
var {}x, y = 5} = {x: 1}
```

（3）字符串解构赋值
```
const [a, b, c, d, e] = 'hello'
a   // 'h'
b   // 'e'
c   // 'l'
d   // 'l'
e   // 'o'
```

（4）函数参数解构赋值
```
function add ([x, y]) {
    return x + y
}
add([1, 2])
```

##### 3. 函数扩展

（1）函数参数默认值
```
function log (x, y = 'world') {
    console.log(x, y)
}
log('Hello')    // Hello World
log('Hello', 'China')   // Hello China
```
注意：
- 不能有同名参数
- 参数变量是默认声明的，不能用let或const再次声明

（2）rest参数
```
function add (...values) {
    let sum = 0
    for (var val of values) {
        sum +=val
    }
}
add(2, 5, 3)
```

（3）箭头函数
```
var f = v => v;

// 等同于
var f = function (v) {
  return v;
};

// 没有参数
var f = () => return 200

// 一个参数
var f = v => v

// 多个参数
var sum = (num1, num2) => num1 + num2

// 代码块内有多句代码
var check = (x, y) => {
    console.log(x, y)
    return x + y
}
```
注意：
- 箭头函数没有自己的this对象
- 不可以当作构造函数
- 不可以使用arguments对象
- 不可以使用yield命令，因此箭头函数不能用作 Generator 函数

##### 4. 数组扩展
（1）复制数组
```
const a1 = [1,2]
const a2 =[...a1]   // 这种复制属于深拷贝
```

（2）合并数组
```
const arr1 = ['a', 'c']
const arr2 = ['d,']
[...arr1, ...arr2]  // ['a', 'c', 'd']
```

（3）Array.from()
Array.from方法用于将两类对象转为真正的数组

（4）Array.of()
##### 5. 对象扩展
（1）属性的简洁表示
```

```

##### 6. 扩展运算符

##### 7. symbol

##### 8. 迭代器

##### 9. 生成器

##### 10. promise
（1）含义
Promise 是异步编程的一种解决方案，所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果

（2）Promise对象有两个特点
- 对象的状态不受外界影响

- 一旦状态改变，就不会再变，任何时候都可以得到这个结果

（3）基本用法
```
const promise = new Promise((resolve, reject) => {
    if (/* 异步操作成功 */) {
        resolve(value)
    } else {
        reject(error)
    }
})
```
- Promise对象是一个构造函数，用来生成Promise实例
- Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject
- resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；
- reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

##### 11. set map

##### 12. class
（1）含义
ES6 的class可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已

（2）定义一个class
```
class point {
    // 构造方法
    constructor (x, y) {
        this.x = x
        this.y = y
    }
    toString () {
        return '(' + this.x + ', ' + this.y + ')';
    }
}
```
ES6 的类，完全可以看作构造函数的另一种写法
```
class Point {
  // ...
}

typeof Point // "function"
Point === Point.prototype.constructor // true
```
类的数据类型就是函数，类本身就指向构造函数
```
class Bar {
  doStuff() {
    console.log('stuff');
  }
}

const b = new Bar();
b.doStuff() // "stuff"
```
构造函数的prototype属性，在 ES6 的“类”上面继续存在。事实上，类的所有方法都定义在类的prototype属性上面
```
class Point {
  constructor() {
    // ...
  }

  toString() {
    // ...
  }

  toValue() {
    // ...
  }
}

// 等同于

Point.prototype = {
  constructor() {},
  toString() {},
  toValue() {},
};
```

（2）constructor方法
constructor()方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor()方法，如果没有显式定义，一个空的constructor()方法会被默认添加
```
class Point {
}

// 等同于
class Point {
  constructor() {}
}
```

（3）类的实例
```
/定义类
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }

}

var point = new Point(2, 3);

point.toString() // (2, 3)

point.hasOwnProperty('x') // true
point.hasOwnProperty('y') // true
point.hasOwnProperty('toString') // false
point.__proto__.hasOwnProperty('toString') // true
```

##### 13. proxy
（1）含义
Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写

（2）Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”
```
var obj = new Proxy(P{}, {
    get: function (target, proKey, receiver) {
        return Relect.get(target, propKey, receiver)
    },
    set: function (target, proKey, value, receiver) {
        return Relect.set(target, propKey, receiver)
    }
})
```

14. async函数
（1）含义
ES2017 标准引入了 async 函数，它就是 Generator 函数的语法糖
Generator 函数

```
const fs = require('fs');

const readFile = function (fileName) {
  return new Promise(function (resolve, reject) {
    fs.readFile(fileName, function(error, data) {
      if (error) return reject(error);
      resolve(data);
    });
  });
};

const gen = function* () {
  const f1 = yield readFile('/etc/fstab');
  const f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

async函数

```
const asyncReadFile = async function () {
  const f1 = await readFile('/etc/fstab');
  const f2 = await readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

（2）基本用法
async函数返回一个 Promise 对象，可以使用then方法添加回调函数。当函数执行的时候，一旦遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句


本文参考：[ECMAScript 6 入门](https://es6.ruanyifeng.com/#docs)