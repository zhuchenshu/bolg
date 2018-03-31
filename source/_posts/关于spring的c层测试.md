---
title: 关于spring的c层测试及出现问题
date: 2017-07-27 20:18:53
tags:
- spring mvc
---
**最近在学习spring MVC 时在对contruller的测试时遇到问题在此总结**
<!--more-->

    this.mockMvc.perform(put("/StandardDeviceCheckDetail/update/" + standardDeviceCheckDetail.getId().toString())
                .contentType("application/json")
                .content(jsonObject.toString())
                .header("x-auth-token", xAuthToken))
                .andExpect(status().isOk())
                .andDo(document("StandardDeviceCheckDetail_update", preprocessResponse(prettyPrint())));

**如上图代码所示**


1. perform 执行一个RequestBuilder请求，会自动执行SpringMVC的流程并映射到相应的控制器执行处理；
2. contentType 中添加传送数据的类型
3. content 模拟发送的数据
4. header 
5. andDo 添加ResultHandler结果处理器，比如调试时打印结果到控制台（对返回的数据进行的判断
6. andExpect 添加ResultMatcher验证规则，验证控制器执行完成后结果是否正确（对返回的数据进行的判断）
7. status.isOk() // 返回的状态是200
***
    JSONObject jsonObject = new JSONObject();
        jsonObject.put("id", standardDeviceCheckDetail.getId());
        jsonObject.put("calibrationDepartment", "danweib");
**模拟前台写入的数据**

**put("字段"，数据)//把数据传入到字段中**

----------
**遇到的问题**

**返回状态码为402**
**问题原因：  请求的方式（get、post、delete）方法与后台规定的方式不符合。
比如： 后台方法规定的请求方式只接受get，如果用post请求，就会出现 405 method not allowed的提示**

