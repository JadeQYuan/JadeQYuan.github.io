title: ElasticSearch别名(7.17)
description: ElasticSearch别名(7.17)
categories:
  - Elastic
author: Jade
date: 2023-09-18 21:30:00
---

别名是数据流或者索引的另一个名称。
大多数ES API支持在数据流或索引名称的地方使用别名。
别名可以在任何时候修改。

## 别名类型
- 数据流别名。
- 索引别名。

## 添加别名
- POST _aliases  add

## 移除别名
- POST _aliases   remove

## 多个动作

## 在索引创建时添加别名
- 组件模板/索引模板。

## 查看别名
- GET _alias

## 写索引
- is_write_index

## 过滤

## 路由
