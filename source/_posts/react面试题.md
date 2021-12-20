<!--
 * @Author: your name
 * @Date: 2021-10-29 14:12:06
 * @LastEditTime: 2021-12-20 16:32:30
 * @LastEditors: Please set LastEditors
 * @Description: 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
 * @FilePath: /carrblog/source/_posts/react面试题.md
-->
---
title: react面试题
date: 2021-3-18 14:12:06
tags:
---

##### 1. React生命周期？
1）componentWillMount   在渲染之前执行，在客户端和服务器端都会执行
2) componentDidMount    仅在第一次渲染后在客户端执行
3) componentWillReceiveProps()  当从父类接收到 props 并且在调用另一个渲染器之前调用
4) shouldComponentUpdate()  根据特定条件返回 true 或 false。如果你希望更新组件，请返回true 否则返回 false。默认情况下，它返回 false
5) componentWillUpdate()    在 DOM 中进行渲染之前调用
6) componentDidUpdate() 在渲染发生后立即调用
7) componentWillUnmount()   从 DOM 卸载组件后调用。用于清理内存空间