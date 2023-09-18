title: ElasticSearch分词(7.17)
description: ElasticSearch分词(7.17)
categories:
  - Elastic
author: Jade
date: 2023-09-17 18:00:00
---

- 文本分词用于支持全文检索。

- 标记化
- 规范化
- 自定义分词器

## 概念
### 文本分词概念
- 不管是内置的还是自定义的分词器，都包含三个低级别的构建块：字符过滤器、分词器和标记过滤器。

#### 字符过滤器
流式接受文本，并添加、移除或者修改字符。

#### 分词器
接受流式字符，将其分解为单个标记，并输出标记流。

#### 标记过滤器
接收标记流，并添加、移除或修改标记。

### 索引和查询分词
文本分词发生在两个地方：索引，查询。
可以指定不同的分词器。

### 词干提取
- 单词简化为其词根形式的过程，可以确保在搜索过程中匹配单词的变体。
- 词干提取依赖于语言。
- 词干提取在标记过滤器中处理。 
- 算法词干提取器，字典词干提取器。

### 标记图
- 当分词器分解标记的时候，也记录了每个标记的位置及长度。
- 有些标记过滤器可以添加标记。
- 有些标记过滤器可以跨多个位置添加标记。

## 配置分词器
- 默认使用standard分词器。

### 测试分词器
- POST _analyze

### 使用内置分词器
- 无需配置。

### 自定义分词器
- 0个或多个字符过滤器。
- 1个分词器。
- 0个或多个标记过滤器。

### 指定分词器
- text类型，索引或查询时。

## 内置分词器
- Standard 
- Simple
- Whitespace
- Stop
- Keyword
- Pattern
- Language
- Fingerprint

## 分词器
### 全词分词器
- Standard
- Letter
- Lowercase
- Whitespace
- UAX URL Email
- Classic
- Thai

### 部分单词分词器
- N-Gram
- Edge N-Gram

### 结构化分词器
- Keyword
- Pattern
- Simple Pattern
- Char Group
- Simple Pattern Split
- Path

## 标记过滤器

## 字符过滤器
- HTML Strip
- Mapping
- Pattern Replace

## 规范化

