---
title: BeanValidation
categories:
  - Java
tags:
  - How
  - validation
description: BeanValidation
date: 2020-02-05 11:04:49
---

## Bean Validation
	Bean Validation是一个运行时的数据验证框架，为JavaBean验证定义了相应的元数据模型和Api。
|JSR版本|Bean Validation版本|发布时间|hibernate实现版本|apache BLal实现版本|
|-|-|-|-|-|
|303|1.0|2009年javaee 6|4.3.1.Final|0.5|
|349|1.1|2013年javaee 7|5.1.1.Final|1.1.1|
|380|2.0|2017年javaee 8|6.0.1.Final|2.0.3|

## Hibernate Validation
	hibernate validation是对这个规范的实践，他提供了相应的实现，并增加了一些其他校验注解(后期规范更新，hibernate将重复的标记了@Departure)，他们位于org.hibernate.validator.constraints包下。
## Spring Validataion
	spring validation对hibernate validation进行了二次封装，在springmvc模块中添加了自动校验，并将校验信息封装进了特定的类（BindingResult）中。
## @Validated 和 @Valid 的区别
- @Validted 支持分组校验，@Valid不支持。
- @Valid支持嵌套验证，@Validated不支持。
- @Validated可以将校验结果绑定到BindingResult中，而不抛出异常。
	必须一个校验对象一个BindingResult，一一对应且紧随其后。
- 在没有分组校验及嵌套校验的情况下， 效果一致。

#### 参考
	https://beanvalidation.org

<p style="text-align: center"><strong>END</strong></p>
