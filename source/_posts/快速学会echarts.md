---
title: 快速学会echarts

date: 2021-2-20 14:49:37
tags:
---
1. 使用步骤
(1）引入echarts.js文件
(2) 准备一个呈现图表的盒子
(3）初始化echarts实例对象
(4）准备配置项
(5）将配置设置给echarts实例对象

2.演示代码
```
<html>
<head>
<meta chartset="utf-8">
// 步骤1:引入echarts.js文件
<script src=“lib/echarts.js"></script>
</head>
<body>
<!— 步骤2:准备一个呈现图标的盒子 -->
<div id="app" style="width: 600px; height: 400px"></div>
<script>
    <!--步骤3: 初始化实例对象-->
    var mCharts = echarts.init(document.getElementById(‘app’)
    <!--步骤4: 准备配置—>
    var options = {
        xAxis: {
            type: ‘category’,
            data: [‘carr’, ‘jack’, ‘lily']
        },
        yAxis: {
            type: ‘value'
        },
        series: [
            {
                name: ‘语文’,
                type: ‘bar’,
                data: [90, 80, 70]
            }
        ]
    }
    <!—步骤5: 将配置项设置给echarts实例—>
    mCharts.setOption(option)
</script>
</body>
</html>
```

3. 配置说明
xAxis   // 类目轴
yAxis   // 数值轴
series  // 系列列表
title   // 图表标题
tooltip // 鼠标滑过或点击柱时的提示
toolbox // 导出、重置、视图
legend  // 图例

// 配置演示
```
// 图表标题
title: {
    text: '成绩展示',
    textStyle: {
        color: 'red',
    },
    borderWidth: 5,
    left: 30,
    top: 10
}

// 鼠标滑过或点击柱时的提示
tooltip: {
    trigger: 'item' | 'axis',   // 触发类型
    triggerOn: 'mouseover' | 'click'    // 触发时机
    formatter: '{a}的成绩是{b}' // 自定义显示类容
}

// 图例
legend: {
    data: [‘语文’, '数学']
}
```
4. 配置柱状图
```
var options = {
    title: {
        text: '柱状图'
    },
    tooltip: {},
    legend: {
        data:['销量']
    },
    xAxis: {
        data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
    },
    yAxis: {},
    series: [{
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20]
    }]
}
```
![效果展示](bar.png)

5. 配置折线图
```
var options = {
    title: {
        text: '折线图'
    },
    xAxis: {
        type: 'category',
        // 是否贴紧Y轴边缘
        boundaryGap: false,
        data: ['一月', '二月', '三月']
    },
    yAxis: {
        // 对与值比较大，而相差又比较小的值，会显得折线波动不明显，将scale设为true，会以最小值作为起始值
        scale: true
    },
    series: [
        {
            type: 'line',
            data: [3000, 2880, 4000],
            markPoint: {
                // 显示最大最小值
                data: [
                    {
                        type: 'max'
                    },
                    {
                        type: 'min'
                    }
                ]
            },
            markLine: {
                // 显示平均值
                data: [
                    {
                        type: 'average'
                    }
                ]
            },
            // 标记指定区间
            markArea: {
                data: [
                    [
                        {
                            xAxis: '一月'
                        },
                        {
                            xAxis: '二月'
                        }
                    ]
                ]
            },
            // 将折线变为平滑曲线
            smooth: true,
            // 折现样式 color: 颜色 type: solid 实线 dashed 点线 
            lineStyle: {
                color: 'green',
                type: 'dashed'
            },
            // 折线区间填充样式
            areaStyle: {
                color: 'pink'
            }
        }
    ]
}
```
![效果展示](line.png)

6. 配置散点图
```

```

7. 配置饼图
```
var options = {
    title: {
        text: '饼图'
    },
    series: [
        {
            type: 'pie',
            data: [
                {
                    name: '淘宝',
                    value: 1000
                },
                {
                    name: '京东',
                    value: 1300
                },
                {
                    name: '拼多多',
                    value: 1200
                },
            ],
            laebl: {

            },
            // radius: 20,
            // radius: ['50%', '70%'],  // 设为圆环图，第一个是内圆半径，第二个是外圆半径
            roseType: 'radius'  // 设为南丁格尔图
        }
    ]
}
```
![效果展示](pie.png)

8. 配置雷达图
```

```

9. 配置仪表盘
```

```
