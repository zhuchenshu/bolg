---
title: springmvc 注释及部分语句的记录
date: 2017-07-29 20:31:21
tags:
- spring mvc
---
@API系列 PagingAndSortingRepository 接口 logger日志输出
<!--more-->

**此博客主要借鉴前人经验，如有不当，敬请指教**

1. Spring MVC 集成 Swagger

  1）.@API表示一个开放的API，可以通过description简要描述该API的功能，一般和 Spring 的 @Controller一起

  2）.在一个@API下，可有多个@ApiOperation，表示针对该API的CRUD操作。在ApiOperation Annotation中可以通过value，notes描述该操作的作用，response描述正常情况下该请求的返回对象类型。

  3).在一个ApiOperation下，可以通过ApiResponses描述该API操作可能出现的异常情况

  4).@ApiParam用于描述该API操作接受的参数类型
     @ApiModel用来描述封装的参数对象与返回的参数对象
     @ApiModelProperty描述ApiModel的属性

	[https://github.com/albertchendao/demos/tree/master/java/spring/HelloWorld-MVC-Swagger](https://github.com/albertchendao/demos/tree/master/java/spring/HelloWorld-MVC-Swagger)
2. springdate 接口之  PagingAndSortingRepository 

 * PagingAndSortingRepository 接口继承于 CrudRepository 接口，拥有CrudRepository 接口的所有方法， 并新增两个方法：分页和排序。 但是这两个方法不能包含筛选条件*

	[http://blog.csdn.net/zgf19930504/article/details/50537225](http://blog.csdn.net/zgf19930504/article/details/50537225)
	[http://blog.csdn.net/u022812849/article/details/42752547](http://blog.csdn.net/u022812849/article/details/42752547)

3. Java日志框架

	**添加logger进行日志输出**

	[http://blog.csdn.net/anialy/article/details/8529188](http://blog.csdn.net/anialy/article/details/8529188)
	[http://www.cnblogs.com/ywlaker/p/6124067.html](http://www.cnblogs.com/ywlaker/p/6124067.html)

