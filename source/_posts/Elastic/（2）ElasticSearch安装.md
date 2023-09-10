title: ElasticSearch安装
description: ElasticSearch安装
categories:
  - Elastic
author: Jade
date: 2023-09-10 20:30:00
---

## Linux下安装
- 下载
- 解压
- 运行

## Windows下安装
- 下载
- 解压
- 运行

## Java（JVM）版本
- ElasticSearch中内置了OPENJDK，推荐使用内置JVM。
- 使用ES_JAVA_HOME环境变量替换内置Java。
- 替换内置Java需注意Java版本。
- 内置JVM是ElasticSearch的一部分，会随着ES一起更新，并负责解决安全事项及bugs。
- 内置JVM在jdk目录下，如果使用自定义JVM需要移除。

## 重要配置
### Path
- data目录，存储数据。
- log目录，存储日志。
- 默认在$ES_HOME目录下。
- $ES_HOME目录下的文件在升级过程中存在删除风险。
- 强烈推荐在yml中配置path.data与path.logs，不要放在$ES_HOME目录下。

### -多路径配置-
- ~~在7.13.0中弃用。~~
- 在多个配置路径中都保存。
- 如果有一个路径磁盘使用率过高，则所有路径都不能添加分片。
- 推荐添加多个节点，而不是多个路径。

### 多路径配置迁移
- 使用硬件/软件虚拟化。
- 迁移，滚动升级。
  - 关闭节点
  - 修改配置
  - 启动节点
  - 下个节点...

### 集群名称配置
- cluster.name
- 只有节点配置集群名称时才能加入到集群中。
- 集群名称默认为elasticsearch。
- **不要在不同的环境中使用相同的集群名称，避免节点加入到错误的集群。**

### 节点名称
- node.name
- 节点名称在许多API中会返回。
- 节点名称默认为主机名。

### 网络配置
- network.host
- 默认使用127.0.0.1。
- **配置后表示在使用生产模式，而不是开发模式。**

### 发现和集群信息配置
- discovery.seed_hosts
- 生产模式按需配置。
- 开箱急用，默认扫描同服务下9300~9305端口。
- 发现其他服务下的节点，需要配置。
- 列表。
- 可配置IP/IPV6地址，域名及端口。
- 默认端口9300，可配置。
---
- cluster.initial_master-nodes
- 如果master-eligible节点没有固定的名称或者地址，可以使用配置动态发现。
- 自动引导本质上不安全。
- 通过配置的节点可以被优先选举为master节点。
- **启动成功之后移除每个节点中的配置。**
- **不要在重启集群或添加新节点时使用该配置。**
- 配置必须与节点名称保持一致。

### 堆大小配置
- ES根据节点角色及内存大小，自动设置堆内存大小。（要求Java14）
- 推荐使用自动计算。

### 堆转存路径设置
- 内存溢出时转存到数据目录。
- Linux、Windows、MacOS默认在安装目录下的root目录。
- jvm.options

### GC日志设置
- jvm.options

### 临时目录
- /temp

### JVM错误级别日志
- Linux、Windows、MacOS默认在安装目录下的logs目录。
- jvm.options

### 集群备份
- 快照。

## 安全配置

## 安全审计配置

...
