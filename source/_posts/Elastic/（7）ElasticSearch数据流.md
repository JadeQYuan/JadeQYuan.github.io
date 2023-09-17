title: ElasticSearch数据流
description: ElasticSearch数据流
categories:
  - Elastic
author: Jade
date: 2023-09-17 21:30:00
---

日期流运行根据时间跨多个索引存储数据。

## 日期流
### 支持索引
自动生产支持索引。
需要索引模板。

### 读请求
路由到所有支持索引。

### 写索引
只能写数据到最新的索引。

### 滚动
推荐使用ILM自动滚动。也可以手动滚动。

### 代
每个数据流追踪它的代数。

### 只追加
通过update by query或delete by query更新或查询。

## 设置数据流
- 创建索引生命周期策略。
- 创建组件模板。
- 创建索引模板。
- 创建数据流。
- 安全数据流。

## 使用数据量


## 更改数据流上的配置
