title: ElasticSearch
categories:
  - Elastic
description: ElasticSearch
author: Jade
date: 2022-06-12 08:29:00
---

V7.17.3

## 全文检索
### 数据分类
- 结构化数据 固定格式、有限长度
- 非结构化数据 不定长，无固定格式
- 半结构化数据 结合

## 搜索分类
- 结构化数据： 关系型数据库
- 非结构化数据： 顺序扫描/全文检索

## 全文检索
- 分词
- 索引

## 倒排索引
- 正排 id -> 内容
- 倒排 关键词 -> id
- 倒排索引 数据 -> 分词 -> 去重 -> 排序

## ElasticSearch
- 分布式、RestFul风格的搜索和数据分析引擎，用Java开发。

- Lucene，单机版的搜索引擎，不支持水平扩展，只针对Java语言。
- 2004年，基于Lucene开发了Comparse。
- 2010年，重命名为ElasticSearch。

## 版本新特性

## 选型
- Solr
- ElasticSearch

## Elastic Stack
解决方案，搜索、日志分析、指标分析、安全分析。
- ElasticSearch
- Logstash
- Kibana
- Beats

## 环境
- ES5 - JDK 8.0
- ES6 - JDK 11
- ES7 内置JDK，配置优先级： ES_JAVA_HOME > JAVA_HOME > ES_HOME

## 配置
### elasticsearch.yml
- cluster
- node
- path
- Host
- Network
### JVM 配置
占用内存较大。
- -Xms
- -Xmx

## 索引操作
索引命名必须小写，不能以_开头
- 创建索引 [PUT /index] {}
- 删除索引 [DELETE /index]
- 修改索引 [PUT /index/_setting]
- 查询索引 [GET /index/..]
- 是否存在 [HEAD /index]

## 索引属性
- aliases
- mapping
- settings

## 术语
- 索引
- 文档

### 文档元数据
- _index
- _type
- _source
- version
- seq_no 解决并发写数据的问题
- primary_term  解决并发写数据的问题

## 文档操作
- 添加文档 [PUT/POST /index/[_doc/_create]/id]
  有id时创建新文档，删除旧文档。全局更新。
- 修改文档 [POST /index/[_update/_updateByQuery]/id]
- 批量操作 [POST _bulk] 偶数行参数 可以操作不同的index
- 批量读取 [GET [_mget/_msearch]]

### 查询
#### 检索原理
- 索引
- 磁盘IO与预读  局部预读性原理
- 倒排索引 单词词典、倒排列表、倒排索引项

#### Query DSL
- GET /index/_doc/_search _doc省略后kibana有提示
- 默认只返回10条数据，默认from+size<10000
- 只有text类型分词
- from、size 分页
- 分页查询scroll
- sort 排序 （_score 为null）
- _source 指定返回某些字段
- match_all 查询所有数据
- match 对关键字进行分词，然后进行匹配（默认or，可改为and）(其它参数)
- match_phrase  短语匹配，要求分词是连续的（slop指定间隔个数）
- multi_match 多字段匹配，一个查询条件多个字段
- query_string 
- simple_query_string + | - 替代 AND OR NOT
- term filed.keyword 关键词查询，不分词，精确匹配 (term必须使用keyword)  使用filter避免算分
- prefix 前缀搜索，匹配分词的前缀，而不是文本的前缀
- wildcard 通配符查询，匹配分词
- range 范围查询 （当前时间now的用法）
- ids 多id查询
- fuzzy 模糊查询，针对错别字的情形 fuzziness（最大2）：错误字数、prefix_length：前缀匹配长度
- highlight 高亮查询，让符合条件的关键字高亮 可自定义样式
- 相关性及算分 排序  算法ES5之前使用TF-IDF（同一个词反复出现，分数会很高），之后使用BM25
- explain true 查看算分公式
- bool 组合查询 must（算分）、should（算分）、must_not（不算分）、filter（不算分） 分数汇总

## Mapping
- dynamic mapping text类型会自动增加子keyword属性
- 静态映射、动态映射、strict映射 新增字段不同实现
- _reindex 重建索引、别名  建新索引 -> reindex -> 删旧索引 -> 使用别名  （文档会怎样？）
- index template 只在索引被创建的时候有用

