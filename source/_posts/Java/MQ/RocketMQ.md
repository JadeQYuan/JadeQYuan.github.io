title: RocketMQ
categories:
  - Java
  - MQ
description: RocketMQ
author: Jade
date: 2022-06-11 19:00:00
---

## 消息中间件
- 异步解耦
- 流量消峰
- 数据分发

## 发展历程
2011 MetaQ 1.0, 阿里基于kafka的设计用Java完全重写。
2012 MetaQ 2.0 
2012 从内部开源出来 RocketMQ 3.0
2016 捐赠给Apache，RocketMQ 4.0

## 角色
- NameServer 注册中心 （集群部署）
- Broker 消息存储 （主从部署）
- Produce 生产者 （集群部署）
- Consumer 服务者 （集群部署） 

## 基本概念
- 主题（Topic）
- 分组（Group）  一般作用于事务消息 
- 消息队列（MessageQueue） 一个Queue对应一个消费者
- 偏移量（Offset）

## 安装
4.8.0
- windows修改runbroker.cmd，CLASSPATH添加“”
- Linux安装修改conf/broker.conf，添加brokerIP，修改runbroker.sh中的堆内存大小，添加-c参数指定配置文件
- 安装dashboard/console

## 普通消息发送
- 同步消息（send（Message））：发送-返回结果，确保消息发送成功。
- 异步发送（send（Message， SendCallBack））：通过异步监听，回调。 适合发送数据量比较大。
- 单向发送（sendOneWay）：没有响应。

## 普通消息消费模式
- 集群消费（默认模式）： 同一个group下，每个消息只会被消费一次。消费队列在Broker中保存。
- 广播消费： 每一个实例都会消费一遍。 不支持顺序消息，重置消费路径。消费队列保存在消费者客户端（客户端重启从最新的消息开始消费）。

## 顺序消息
- 全局顺序消息 指定只使用一个Queue。
- 部分顺序消息 不同的Queue进项标识。MessageQueueSelector。发生异常 SUSPEND, 不能设置为重新发送。

## 延时消息
- Message.setDelayTimeLevel。 延时等级-延时时间。 订单支付

## 批量消息
- send(Collection<Message>)。
- 不能超过4M。 拆分

## 过滤消息
- Tag过滤 
- SQL过滤 MessageSelector.bySql  Message.putUserProperty

## 消息发送方法和属性
- producerGroup： 事务消息比较重要
- setDefaultTopicQueueNums 8 
- setSendMsgTimeout 3s
- setCompressMsgBodyOverHowMuch  4k 超过启用压缩
- setRetryTimesWhenSendFailed  2 总共执行3次
- setRetryTimesWhenSendAsyncFailed  2 总共执行3次
- setRestyAnotherBrokerWhenNotStoreOK false 没有存储成功是否发送到另外一个broker
- setMaxMessageSize 4M 允许发送的最大消息长度

## 消息消费方法和属性
- consumerGroup
- setMessageModel 集群/广播
- setConsumerFromWhere LAST_OFFSET 指定消费开始偏移量
- setConsumerThreadMin 20 消费者最小线程数
- setConsumerThreadMax 20 消费者最大线程数
- setPullInterval 0
- setPullBatchSize 32
- setMaxReconsumeTimes -1 16，重试次数，死信消息
- setConsumerTimeout 15min 消费超时时间

- subscribe
- registerMessageListener  MessageListenerOrderly 顺序消息
- ACK

## 高可用
- 单master模式
- 多master模式
- 多master多slaver同步（同步复制，消息保存复制成功才会返回）
- 多master多slaver异步（异步复制）

- 刷盘 同步刷盘与异步刷盘
- 一般采用同步复制+异步刷盘  复制速度 > 刷盘速度

## 存储设计
- 顺序、重复 问题

## Q
- Consumer ACK确认？
- 消费者模式都消费者指定？不同消费者指定不同的模式？