---
title: canvas使用
date: 2021-10-29 14:57:18
tags:
---
1. 基本使用
```
<!-- HTML-->
<canvas id="myCanvas" width="500" height="500"></canvas>
```
```
var canvas = document.getElementById('#myCanvas')
var ctx = canvas.getContext('2d')   // 获取2d上下文对象
ctx.fillStyle = '#cccccc'
// 绘制填充矩形
ctx.fillRect(20,20,100,100)
// 绘制矩形边框
ctx.stockRect(x,y,width,height)
// 清除指定矩形区域
clearRect(x,y,width,height)
// 绘制路径
beginPath()
moveTo(x, y)
closePath()
stroke()
```