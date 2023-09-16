title: ElasticSearch映射
description: ElasticSearch映射
categories:
  - Elastic
author: Jade
date: 2023-09-16 10:15:00
---

映射定义了文档中包含的字段，及字段是如何存储和被索引的。
映射也包括元数据字段。
可以使用动态索引或明确索引来定义数据。

## 动态映射
- 无需创建索引，根据插入的文档字段类型自动创建索引。
- 动态字段映射只有在字段有正确的值的时候才会添加，当字段为null或空数组时不会添加。

### 动态字段映射
可以根据dynamic参数（true/runtime）明确指定动态创建索引。

#### 字段类型
| JSON           | dynamic:true           | dynamic:runtime |
|----------------|------------------------|-----------------|
| null           | 不添加字段                  | 不添加字段           |
| true/false     | boolean                | boolean         |
| double         | float                  | double          |
| long           | long                   | long            |
| object         | object                 | 不添加字段           |
| array          | 数组中第一个值的类型             | 数组中第一个值的类型      |
| 日期类型的字符串       | date                   | date            |   
| 数字类型的字符串       | float/long             | double/long     |   
| 无法转换成日期或数字的字符串 | text，并且有一个.keyword的子类型 | keyword         |   

- 在文档级别和对象级别上都可以设置是否动态索引。
- 动态索引设置为false，将拒绝无法识别类型的字段。
- 可以使用更新API在更新已存在字段上的dynamic配置。
- 可以使用动态模板来检测日期类型及数字类型。

#### 日期检测
- 默认打开。
- 默认值： dynamic_date_formats： [ "strict_date_optional_time","yyyy/MM/dd HH:mm:ss Z||yyyy/MM/dd Z"]。
- 关闭日期检测，mapping: date_detection: false。
- 自定义日期检测格式， dynamic_date_formats: [...]。
  
#### 数字检测
- 自动检测浮点型和整形数字。
- 默认关闭。
- 打开数字检测，mapping: number_detection:true。

### 动态模板
- 动态模板用于控制动态映射如何生成。
- 匹配条件： match_mapping_type,match,match_pattern,unmatch,path_match,path_unmatch

#### 动态模板校验
// TODO

#### ...

### 显示映射
- 通过创建索引API指定显示的映射关系。
- 通过更新API添加字段映射。
- 无法更新已经存在的字段映射关系。
- 流式处理/重索引。
- 使用别名，而不是修改字段名称。
- 通过查看API查看映射关系。
- 通过API查看执行字段的映射关系。

### 运行时字段
- 添加字段而不需要重索引。
- 不需要理解它的结构？？？
- 覆盖原查询返回的值。
- 不需要修改依赖的模块？？？

- 可以通过mapping或者request定义。
- 运行时字段不会在_source中显示。

- 运行时字段没有被索引。
// TODO

### 字段类型

### 元数据字段
创建索引映射关系时可以自定义元数据字段。

- 唯一
  - _index
  - _type
  - _id
- 来源
  - _source
  - _size
- 文档计数
  - _doc_count
- 索引
  - _field_names
  - _ignored
- 路由
  - _routing
- 其它
  - _meta
  - _tier

### 映射参数

- analyzer
- boost
- coerce
- copy_to
- doc_values
- dynamic
- eager_global_ordinals
- enabled
- fielddata
- fields
- format
- ignore_above
- ignore_malformed
- index_options
- index_phrases
- index_prefixes
- index
- meta
- normalizer
- norms
- null_value
- position_increment_gap
- properties
- search_analyzer
- similarity
- store
- term_vector

### 映射限制设置
- index.mapping.total_fields.limit: 1000
  - 默认1000。
- index.mapping.depth.limit: 20
- index.mapping.nested_fields.limit: 50
- index.mapping.nested_objects.limit: 10000
