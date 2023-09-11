title: Mysql 填坑
categories:
  - Mysql
description: Mysql 填坑
author: Jade
date: 2021-06-24 17:07:00
---

## mysql left on where
过程： from + left 生成中间表 -> 对中间表进行where过滤
on 是在生成中间表的时候的条件， 不管on后的条件是否满足，都会返回主表的所有数据
where 是对中间表过滤的条件

## count(1) VS count(*) VS count(列)
基于InnoDB。  
Mysql对count做了处理，查询效率没差别。
