title: Stream原理
categories:
  - Java
description: Stream原理
author: Jade
date: 2020-09-09 16:32:00
---

## stream
Java 8 中定义了四种流，分别是Stream、IntStream、LongStream、DoubleStream。每种流的操作、参数等都有区别。
### BaseStream
所有流接口的父级接口。
### Streams
工具类。
### StreamSupport
创建流的工具，多用于类库

## PipelineHelper
流水线，通过其将流串起来。
### AbstractPipeline
抽象类，定义了流水线串联起来的属性，及一些方法。
### Pipeline
与流类型，也分为四类。ReferencePipeline、IntPipeline、LongPipeline、DoublePipeline。
#### ReferencePipeline
引用类型的流水线，抽象类，其实现类主要有，Head、StatelessOp、StatefulOp，分别表示第一个、无状态的和有状态。

## OP
操作
### 中间操作
#### 有状态的操作
- distinct
- sorted
- limit
- skip
#### 无状态的操作
- map
- filter
- peek
### 结束操作
TerminalOP。
#### 短路操作
- match
- find
#### 非短路操作
- foreach
- reduce


## Sink
真正的执行者。
### TerminalSink
标识是结束操作。

## Node
返回值。

## Task
通过ForkJoinTask来实现并行流的处理。

## 流程
### 编码流程
1. 创建一个stream
2. 添加中间操作，包括有状态、无状态操作
3. 添加结束操作
4. 如果有返回值，接收返回值

### 实现流程
1. 创建steam，其类型为Head
2. 每一步中间操作，创建一个新的stream，其类型为StatelessOp或StatefulOp，并在新的steam中保存上一个stream的引用
3. 对于结束操作，创建一个新的TerminalSink
4. 通过stream中的引用，逆序对每一个中间操作创建一个Sink，因为Sink继承自Consumer，在accpet中调用下流sink
5. 接收返回值

