title: ElasticSearch索引
description: ElasticSearch索引
categories:
  - Elastic
author: Jade
date: 2023-09-10 21:15:00
---

索引模块是创建并控制与索引相关方面的模块。
## 索引设置
- 可以按索引设置索引级别。
- static级别的设置，只能在创建和索引关闭期间设置。
- dynamic级别的设置，可以在正在使用的索引上设置。
- 更新静态/动态索引设置可能会导致无法纠正的错误。

## 静态索引设置
以下静态索引设置不跟任何特定的索引模块相关。
- index.number_of_shards
  - 默认1，最大1024（可修改）。
  - 只能在创建时设置，无法在闭合索引上修改。
- index.number_of_routing_shards
  - 拆分索引时使用。
- index.codec
  - 压缩编码格式。
  - 默认LZ4。
- index.routing_partition_size
  - 默认1。
  - 只能在索引创建时设置。
- index.soft_deletes.enabled
  - 默认true。
  - 只能在索引创建时设置。
- index.soft_deletes_retention_lease.period
  - 默认12h。
- index.load_fixed_bitset_filters_eagerly
  - 默认true。
- index.shard.check_on_startup
  - 仅限专家用户。
  - false、checksum、true。

## 动态索引设置
以下动态索引设置不跟任务特定的索引相关。
- index.number_of_replicas
  - 默认1。
- index.auto_expand_replicas
  - 默认false。
  - 0-5/all/0-all。
  - 基于集群中节点的数量。
- index.search.idle.after
  - 默认30s。
- index.refresh_interval
  - 默认1s。
- index.max_result_window
  - from + size。
  - 默认10000。
- index.max_inner_result_window
  - from + size。
  - 默认100。
  - Inner hits & Top hit aggregations。
- index.max_rescore_window
  - 默认10000。
- index.max_docvalue_fields_search
  - 默认100。
- index.max_script_fields
  - 默认32。
- index.max_ngram_diff
  - 默认1。
- index.max_shingle_diff
  - 默认3。
- index.max_refresh_listeners
- index.analyze.max_token_count
  - 默认10000。
- index.highlight.max_analyzed_offset
  - 默认1000000。1000000
- index.max_terms_count
  - 默认65536。
- index.max_regex_length
  - 默认1000。
- index.query.default_field
  - 默认*。
- index.routing.allocation.enable
- index.routing.rebalance.enable
  - 默认all。
  - all、primaries、replicas、none。
- index.gc_deletes
  - 默认60s。
- index.default_pipeline
- index.final_pipeline
- index.hidden
  - 默认false。

## 其他设置
### 分词器设置
- 参考文本分词器。

### 索引分片分配
控制分片分配到节点的方式。
#### 分配过滤

#### 延迟分配
#### 分片总数
#### 数据层分配

## 



