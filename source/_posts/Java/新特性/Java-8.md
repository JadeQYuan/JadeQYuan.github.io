title: Java 8
categories:
  - Java
  - 新特性
tags:
  - How
  - ''
description: Java 8
author: Jade
date: 2020-09-14 13:23:00
---

## 简介
Oracle公司于2014年3月18日发布Java 8。它支持函数式编程，新的JavaScript引擎，新的如期API，新的Stream API等。

## 新特性
### 语言
- lambda 表达式和函数式接口
- 接口的默认方法和静态方法
- 方法引用
- 重复注释
- 更好的类型推断
- 注解的扩展 （扩展了注解可以使用的范围，包括：局部变量，泛型，超类，接口实现，方法的exception声明等）

### 编译器
- 参数名字

### JDK
- Optional
- Stream
- 时间日期API
- Nashorn javascript引擎
- Base64
- 并行数组 （增加了支持并行的数组处理）
- 并发 （新增StampedLock、DoubleAccumulator、DoubleAdder、LongAccumulator、LongAdder等）

### 工具
- Nashorn引擎 jjs
- 类依赖分析工具 jdeps

### JVM
- JVM内存永久区被metaspace替换，JVM参数 -XX:PermSize 和 -XX:MaxPermSize 被 -XX:MetaSpaceSize 和 -XX:MaxMetaSpaceSize 代替。


<p style="text-align: center"><strong>END</strong></p>