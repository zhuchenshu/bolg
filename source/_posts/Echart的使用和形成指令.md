---
title: Echart的使用和形成指令
date: 2018-03-31 10:29:50
tags: angularjs
---
Echart的使用与将图标形成指令
<!--more-->

完成后如下图所示

![image](http://upload-images.jianshu.io/upload_images/5451241-e0d64bffd1c3eb78?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**1\. Echart的使用**

[官网地址](http://echarts.baidu.com/tutorial.html#5%20%E5%88%86%E9%92%9F%E4%B8%8A%E6%89%8B%20ECharts)

官网教程引入，根据教程可以很简单的完成实例的引入，我主要写关于百分率样式的配置

代码入下所示

```
var option = {
                    title: {
                        text: {}
                    },
                    color: ['#62CB31'],
                    tooltip: {
                        trigger: 'item',
                        formatter: '{b}:\n{c}%'
                    },
                    xAxis: [{
                        type: '',
                        data: [],
                        axisTick: {
                            alignWithLabel: true
                        }
                    }],
                    yAxis: {
                        type: 'value',
                        min: '',
                        max: '',
                        axisLabel: {
                            show: true,
                            interval: 'auto',
                            formatter: '{value} %'
                        }
                    },
                    series: [{
                        name: '',
                        type: 'bar',
                        data: [],
                        itemStyle: {
                            normal: {
                                color: function(params) {
                                   var colorList = CommonService.getChartBarColor();
                                    return colorList[params.dataIndex % colorList.length];
                                },
                                label: {
                                    show: true,
                                    position: 'top',
                                    formatter: '{b}\n{c}%'
                                }
                            }
                        },
                        axisLabel: {
                            show: true,
                            interval: 'auto',
                            formatter: '{value} %'
                        },
                        barWidth: 70
                    }]
                };
```
1.1 y轴的百分比显示
```
axisLabel: {
               show: true,
               interval: 'auto',
               formatter: '{value} %'
}
```
1.2 柱形上的显示与多颜色的加入
```
 itemStyle: {
                            normal: {
                                color: function(params) {
                                   var colorList = CommonService.getChartBarColor();
                                    return colorList[params.dataIndex % colorList.length];
                                },
                                label: {
                                    show: true,
                                    position: 'top',
                                    formatter: '{b}\n{c}%'
                                }
                            }
                        }
```
**2\. 指令的使用**

```
<yunzhi-chart-bar data-chart-name = "chartName" data-chart-xdata="chartXData" data-chart-ymax="chartYMax" data-chart-ymin="chartYMin" data-chart-dar="chartDarData"></yunzhi-chart-bar>
```

外部数据：图表名称，图标x轴，图表y轴，图表bar内容（数据）

在写指令是遇到问题是`$watch`的多监听

解决如下
```
scope.$watch('[chartXdata, chartDar, chartName, chartYmin, chartYmax]', function(newValue) {
                    if (scope.chartDar) {  // 防止第一次数据为空时加载图表
                        $timeout(function() {
                            self.setChart();
                        }, 1000);
                    }
                }, true);
```
把要监听的对象放入数组中，进行多对监听

