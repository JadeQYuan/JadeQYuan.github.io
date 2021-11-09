title: validate
categories:
  - Java
description: validate
author: Jade
date: 2020-07-14 14:15:00
---

## JSR303, JSR-349
JSR303是一项标准,JSR-349是其的升级版本，添加了一些新特性，他们规定一些校验规范即校验注解，如@Null，@NotNull，@Pattern，他们位于javax.validation.constraints包下，只提供规范不提供实现。

@Null 被注释的元素必须为null
@NotNull 被注释的元素必须不为null
@AssertTrue 被注释的元素必须为true
@AssertFalse 被注释的元素必须为false
@Min(value) 被注释的元素必须是一个数字，其值必须大于等于指定的最小值
@Max(value) 被注释的元素必须是一个数字，其值必须小于等于指定的最大值
@DecimalMin(value) 被注释的元素必须是一个数字，其值必须大于等于指定的最小值
@DecimalMax(value) 被注释的元素必须是一个数字，其值必须小于等于指定的最大值
@Size(max, min) 被注释的元素的大小必须在指定的范围内
@Digits (integer, fraction) 被注释的元素必须是一个数字，其值必须在可接受的范围内
@Past 被注释的元素必须是一个过去的日期
@Future 被注释的元素必须是一个将来的日期
@Pattern(value) 被注释的元素必须符合指定的正则表达式

## hibernate validation
hibernate validation是对这个规范的实践（不要将hibernate和数据库orm框架联系在一起），他提供了相应的实现，并增加了一些其他校验注解，如@Email，@Length，@Range等等，他们位于org.hibernate.validator.constraints包下。
@Email 被注释的元素必须是电子邮箱地址
@Length 被注释的字符串的大小必须在指定的范围内
@NotEmpty 被注释的字符串的必须非空
@Range 被注释的元素必须在合适的范围内

## spring validation
spring validation对hibernate validation进行了二次封装，在springmvc模块中添加了自动校验，并将校验信息封装进了特定的类中

* 注意，必须相邻，如果有多个参数需要校验，形式可以如下。valid(@Validated Person person, BindingResult fooBindingResult ，@Validated Bar bar, BindingResult barBindingResult);即一个校验类对应一个校验结果。
* 校验结果会被自动填充
* 不加BindingResult ，会抛出BindException

1. @Validate 和 @Valid 的区别
而
而万能的spring为了给开发者提供便捷，对hibernate validation进行了二次封装，显示校验validated bean时，你可以使用spring validation或者hibernate validation，而spring validation另一个特性，便是其在springmvc模块中添加了自动校验，并将校验信息封装进了特定的类中。这无疑便捷了我们的web开发。
@Validate 支持分组验证，@Valid 支持嵌套验证

2. @Validate 用在方法入参和类上面的区别（能否用在方法上）
4. spring controller 验证
5. 方法参数验证
6. 自定义校验注解

