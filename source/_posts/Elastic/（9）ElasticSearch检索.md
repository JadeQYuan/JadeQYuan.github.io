title: ElasticSearch检索(7.17)
description: ElasticSearch检索(7.17)
categories:
  - Elastic
author: Jade
date: 2023-09-19 21:00:00
---

## 检索
检索就是在ES数据流或索引中请求数据。

### 运行
- GET /{index}/_search

### 定义只在查询中存在的字段
- runtime_mapping

### 通用查询选项
#### Query DSL
- Boolean和其他复杂查询
- 精确匹配
- 全文检索
- 坐标查询

#### 聚合

#### 多数据流和多索引查询

#### 分页查询

#### 查询指定字段
- _source

#### 排序

#### 异步查询

### 查询超时
- 默认不会超时。
- timeout，每个分片查询的超时时间。

### 取消查询

### 追踪总数

### 快速检查

## 折叠检索结果
### 折叠
- collapse

### 展开折叠结果
- inner_hits

### 使用search_after折叠
- search_after

### 二级折叠
- inner_hits

## 过滤检索结果
- boolean过滤器
- 聚合

### 后置过滤器
- post_filter
- 在聚合之后过滤。

### 重新计算过滤结果得分
- rescore

### 查询重评分器

### 多评分器

## 高亮
- highlighting

### 统一高亮器
- Lucene统一高亮器。

### 文本高亮器

### 快速矢量高亮

### 偏移策略

### 高亮设置

## 长时间运行的检索
- 使用异步

## 近实时检索
- 1s内。

## 分页查询
- 默认前10条。
- from、size。

### search_after
- 基于上一页的id，查询下一页。

### 滚动搜索结果
- 不推荐在深度分页时使用滚动，推荐使用search_after。

### 保持检索上下文存活

### 清楚滚动

## 查询内部匹配结果
- parent-join、nested。

### 嵌套内部匹配

### 父子内部匹配

## 查询指定的字段
- fields 
- _source 

## 跨集群检索

## 在多数据流和索引检索

## 分片路由检索

## 检索模板

## 排序检索结果

