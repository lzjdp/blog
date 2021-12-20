---
title: flex使用介绍
date: 2021-10-29 14:30:23
tags:
---

##### 1. Flex布局是什么？
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性

##### 2. 基本概念
采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"
![flex](flex_1.png)
水平的主轴（main axis）
垂直的交叉轴（cross axis
主轴的开始位置  main start
结束位置    main end
交叉轴的开始位置    cross start
个项目占据的主轴空间    main size
占据的交叉轴空间    cross size

##### 3.容器的属性
- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

（1）flex-direction
flex-direction属性决定主轴的方向（即项目的排列方向）
```
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}
```
- row（默认值）：主轴为水平方向，起点在左端。
- row-reverse：主轴为水平方向，起点在右端。
- column：主轴为垂直方向，起点在上沿。
- column-reverse：主轴为垂直方向，起点在下沿。
![flex](flex_2.png)

（2）flex-wrap属性
默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行
```
.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```
- nowrap（默认）：不换行
- wrap：换行，第一行在上方
- wrap-reverse：换行，第一行在下方

（3）flex-flow
lex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap
```
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

（4）justify-content属性
justify-content属性定义了项目在主轴上的对齐方式
```
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```
- flex-start（默认值）：左对齐
- flex-end：右对齐
- center： 居中
- space-between：两端对齐，项目之间的间隔都相等。
- space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
![flex](flex_3.png)

（5）align-items属性
align-items属性定义项目在交叉轴上如何对齐。
```
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```
- flex-start：交叉轴的起点对齐。
- flex-end：交叉轴的终点对齐。
- center：交叉轴的中点对齐。
- baseline: 项目的第一行文字的基线对齐。
- stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
![flex](flex_4.png)

（6）align-content属性
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

- flex-start：与交叉轴的起点对齐。
- flex-end：与交叉轴的终点对齐。
- center：与交叉轴的中点对齐。
- space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
- space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch（默认值）：轴线占满整个交叉轴。
![flex](flex_5.png)

##### 特别说明：
[本文转载自：Flex 布局教程](https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)