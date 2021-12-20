<!--
 * @Author: your name
 * @Date: 2021-10-29 14:25:25
 * @LastEditTime: 2021-12-20 16:22:51
 * @LastEditors: your name
 * @Description: 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
 * @FilePath: /carrblog/source/_posts/css面试题.md
-->
---
title: css面试题
date: 2020-10-29 14:25:25
tags:
---

##### 1.清除浮动的方法？

##### 2.关于BFC?
（1）什么时BFC
BFC（Block Formatting Context）格式化上下文，是web页面中盒模型布局的CSS渲染模式
，指一个独立的渲染区域或者说是一个隔离的独立容器，如果一个元素符合触发BFC的条件，则该元素中的布局
不受外部影响

（2）形成BFC的条件
- 浮动元素：float = left | right | inherit
- 绝对定位元素： position = absolute ｜ fixed
- display = inline-block ｜ table-cell ｜ table-caption
- overflow = hidden ｜ auto｜scroll

（3）BFC特性
- 内部的BOX会在垂直方向上一个接一个的放置
- 垂直方向上的距离由margin决定
- bfc的区域不会与float的元素区域重叠
- 计算bfc高度时，浮动元素也参与计算
- bfc就是页面上的一个独立容器，容器里面的子元素不会影响外面元素


##### 3.未知宽高元素上下左右居中

##### 4.已知元素的上下左右居中

##### 5.display:none 和 visibility: hidden的区别？
display:none 元素后代以及它的所有后代元素都会隐藏，隐藏后元素无法点击，占据的空间消失

visibility: hidden 隐藏元素仍需占据空间，父元素设置visibility: hidden，子元素也会
继承这个属性

##### 6.列举css的几种单位
相对长度
- em    它是描述相对于应用在当前元素的字体尺寸
- rem   是根 em（root em）的缩写，rem作用于非根元素时，相对于根元素字体大小
- vh    viewpoint height，视窗高度，1vh=视窗高度的1%
- vw    viewpoint width，视窗宽度，1vw=视窗宽度的1%
- vmin  vw和vh中较小的那个
- vmax  vw和vh中较大的那个
- %     相对父元素   

绝对长度
- cm    厘米
- mm    毫米
- in    英寸
- px    像素
- pt    point，大约1/72英寸
