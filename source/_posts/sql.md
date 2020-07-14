title: sql
categories:
  - null
tags:
  - How/Why
  - null
description: sql
author: Jade
date: 2020-07-14 14:09:55
---
# SQL
> How


## 概念
混合排序
子查询： 将一个查询（子查询）的结果作为另一个查询（主查询）的数据来源或判断的来源。
相关子查询: 依赖于主查询，多数情况下是子查询的WHERE子句中引用了主查询的表。

## 外键
数据库外键
	保证数据的一致性，完整性
外键功能实现方式
	RESTRICT   	在更新和删除时进行一致性检查
	CASCADE		在更新和删除时级联执行

在使用时不应该一刀切的决定用或者不用外键，应该根据具体的场景做决策。

使用数据库外键会增加数据库压力，不适用数据库外键需由服务层来处理数据一致性。
	
## 连接查询
LEFT JOIN  -> A 
RIGHT JOIN -> B
INNER JOIN -> A ∩ B
FULL JOIN -> A ∪ B


## EXIST 与 IN
后面跟的都是子查询
EXIST 指定一个相关子查询，检测行的存在


## NOT EXIST 与 NOT IN
NOT EXIST 效率比 IN 要高


## 分页查询
当数据量足够大且分页当前页足够大时，查询会很慢，这时可以根据排序字段加条件，用条件来减少数据量。

## 关联更新、删除
UPDATE JOIN ON 

## 提交缩小查询范围
主表连接副表查询，最后limit，可以先对主表做limit查询，最后在关联副表


<p style="text-align: center"><strong>END</strong></p>