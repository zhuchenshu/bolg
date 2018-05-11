---
title: spring hebernate 数据查询
date: 2018-05-11 18:14:56
tags:
---

在使用hebernate的数据查询时总是遇到问题，在此将自己在hebernate中的查询做一下总结


<!--more-->

<!--more-->

1.jpa的数据查询

*   直接使用关键字查询，适合单表查询，简单查询,示例代码如下

    Page<MandatoryInstrument>findAllByStatusAndDepartmentAndNextCheckDateBetween(Byte statusNormal, Department department, Date beginDate, Date endDate, Pageable pageable);

方法的名字相当于查询的方法并配合方法的参数进行数据查询

当前方法意思是在当前实体中根据Status，Department，NextCheckDate（在beginDate与endDate之间）这几个属性都为当前实体的属性，通过这几个条件查询满足条件的实体，最后一个参数pageable代表传入分页信息

[参考文档](https://docs.spring.io/spring-data/jpa/docs/2.0.5.RELEASE/reference/html/)

*   使用@query查询，适合多表查询，和复杂查询

当时遇到问题是：不知道@query里面是存放纯sql语句还是有专门语法，后来查了一下里面的语法不是纯sql语句

<colgroup style="line-height: 1.57143em;"><col data-mce-style="width: 130px;" style="line-height: 1.57143em; width: 130px;"><col data-mce-style="width: 130px;" style="line-height: 1.57143em; width: 130px;"></colgroup>


@Query("select i from #{#entityName} i" +

" where i.deviceSet.department = :department " +

" and i.lastCheckDate between current_date() and :nextDay ")

Page<StandardDevice> findAllByDepartmentAndLastCheckDateBetweenTodayAndNextDay(@Param("nextDay") Date nextDay, @Param("department") Department department, Pageable pageable);


对象比较

i.deviceSet.department = ：department 可以找到当前实体的标准器的部门,并直接与传入的部门参数进行比较

日期处理

i.lastCheckDate between current_date() and :nextDay 检测当前数据的日期是否在今天与下一个时间之间

i.lastCheckDate < current_date() 检测当前数据的日期是否小于今天

多表嵌套查询
多表查询是使用nativeQuery = true里面使用纯SQL语句

```
// 查找属于某个部门的非检定员用户
    @Query(value ="select *" +
            "from user " +
            "where user.id not in " +
            "(select check_personal.user_id from check_personal)" +
            " and user.department_id = :departmentId", nativeQuery = true)
    List<User> findNotCheckUserByDepartmentId(@Param("departmentId") Long departmentId);
```
返回查询数据中的前多少条

`@Query(nativeQuery = true,value = "SELECT  * FROM  sell WHERE sell.id > :lastid  limit :number ")`