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
- 可以使用分配过滤器控制将索引分配在哪个分片上。
- cluster.routing.allocation
  - 动态配置，支持存活的索引从一个节点迁移到另一个节点。
  - 分片只有在不破坏其他路由时才会重新分配。
- node.attr.size
  - small、medium、big。
- index.routing.allocation.include.{attribute}
- index.routing.allocation.require.{attribute}
- index.routing.allocation.exclude.{attribute}
  - _name
  - _host_ip
  - _publish_ip
  - _ip
  - _host
  - _tier

#### 延迟分配
- 当一个节点离开集群时：
  - 将副本分配提升为主分片
  - 分配副本分配代替消失的分片
  - 在剩余的节点中重新平衡分配分配
- 保证集群数据不会丢失，每个分片都是全复制。
- index.unassigned.node_left.delayed_timeout
  - 动态配置。
  - 默认1m。
  - 可在存活的索引上更新。

#### 恢复优先级
- 优先级
  - index.priority（设置且越大越优先）
  - 索引创建日期（越近创建越优先）
  - 索引名称

#### 分片总数
- index.routing.allocation.total_shards_per_node
  - 在一个节点上可分配的最大分片数量。
- cluster.routing.allocation.total_shards_per_node
  - 在每个节点上可分配的最大分片数量。

#### 数据层分配
- index.routing.allocation.include._tier
- index.routing.allocation.require._tier
- index.routing.allocation.exclude._tier
- index.routing.allocation.include._tier_preference

### 索引块
索引块限制在索引上的操作是否可用。
#### 设置 
- index.blocks.read_only true: 只读数据及元数据
- index.blocks.read_only_allow_delete
- index.blocks.read true:无法读取索引
- index.blocks.write true:无法写入索引
- index.blocks.metedata true:无法读取/写入索引元数据
#### API
- PUT /<index>/_block/<block>

### 映射
- 参考Mapping。

### 合并
- ES中的每个分片都是Lucene中的索引。
- index.merge.scheduler.max_thread_count

### 相似模块

### 日志查看
- index.search.slowlog.threshold.query.warn: 10s
- index.search.slowlog.threshold.query.info: 5s
- index.search.slowlog.threshold.query.debug: 2s
- index.search.slowlog.threshold.query.trace: 500ms
- index.search.slowlog.threshold.fetch.warn: 1s
- index.search.slowlog.threshold.fetch.info: 800ms
- index.search.slowlog.threshold.fetch.debug: 500ms
- index.search.slowlog.threshold.fetch.trace: 200ms

### 存储
- index.store.type: hybridfs
  - fs、simplefs、niofs、mmapfs、hybridfs。
- index.store.preload

### Translog

### 保留历史
- index.soft_deletes.enabled
- index.soft_deletes.retention_lease.period

### 索引排序
- index.sort.*
  - index.sort.field
  - index.sort.order
  - index.sort.mode
  - index.sort.missing

### 索引压力
- indexing_pressure.memory.limit

## Q
- index-level shard 
- index-level data tier
- node level
  - primary
  - replica


