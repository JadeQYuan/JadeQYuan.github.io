title: Java SE 9 ~ 11新特性
categories:
  - Java
  - Java平台
description: Java SE 9 ~ 11新特性
author: Jade
date: 2020-07-21 16:39:00
---

### Java SE 9 (2017-09)
- 模块化
- jShell
- 接口可定义private方法 （只能在接口内部调用）
- try with resource 优化
- String, StringBuilder, StringBuffer 中的value由char[]改为byte[]
- List、Set、Map 添加of方法创建只读集合
- InputStream流加强
- StreamAPI takeWhile、dropWhile、ofNullable、iterate
- Optional增加stream()
- 垃圾回收机制

### Java SE 10 (2018-03)
- 局部变量类型推断
- 不可变集合的改进
- 并行全垃圾回收器 G1
- 线程本地握手
- Optional新增orElseThrow()方法
- 类数据共享
- Unicode 语言标签扩展
- 根证书

### Java SE 11 (2018-09-25)
- String API isBlank、strip、stripTrailing、stripLeading、repeat、lines.count
- Optional API isEmpty...
- 局部变量类型推断加强 var上可以加注解
- HttpClient
- 垃圾回收ZGC
