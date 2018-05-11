---
title: ng-select ng-options
date: 2018-05-11 18:17:21
tags:
---
 最近一段时间的项目中遇到了很多的关于下拉框的场景，当时只是模仿原有的项目代码，并没有深入的理解，为此写此博客将该问题深入进行理解。

<!--more-->

<!--more-->

主要是对ng-options的学习

下面现将ng-options的几个典型的用法列出来
在<select>指令中ng-model 与 ng-options 配合使用

ngOption针对不同类型的数据源有不同的用法，主要体现在数组和对象上，因为我们主要使用数组，所以下面主要讲数组。

label for value in array 
这是最简单的一个只是简单的将数组中对象的lable属性显示出来，ng-model的值还是value。

select as label for value in array
这种写法中涉及到as的使用，当前的显示还依然是lable的值，但是ng-model的值已经发生了改变，成为了select中的值

label group by group for value in array
这种写法涉及到group for的使用当前的显示还是lable,但回按照group分组，ng-model的值为value

 label for value in array  track by trackexpr
这条指令涉及到track by 的使用用于唯一确定数组中的迭代项的表达式,当lable相同时，指定唯一的value值与ng-model绑定


当数据源为对象时
label for ( key , value ) in object
为大概使用模式，就是将value改为 ( key , value )如下形式，ng-model默认绑定model

在学习上面几种写法时，发现track by 的使用不太好理解,用官网上的例子说明一下。
This will work:

<select ng-options="item as item.label for item in items track by item.id" ng-model="selected"></select>
$scope.selected = $scope.items[0];

but this will not work:

<select ng-options="item.subItem as item.label for item in items track by item.id" ng-model="selected"></select>
$scope.selected = $scope.items[0].subItem;

第一个你可以通过ng-model来唯一确定数组中的迭代项，items[0]里面包含item.id
第二个你会发现items[0].subItem不能确定item.id