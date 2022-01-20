title: Java 1.0 ~ Java SE 8新特性
categories:
  - Java
  - Java平台
description: Java 1.0 ~ Java SE 8新特性
author: Jade
date: 2020-07-21 16:39:00
---

## Java 1.0 （1996-01-23）
- Classic VM（虚拟机）
- Applet（java小应用程序）
- AWT（java图形设计）

## Java 1.1 （1997-02-19）
- JAR
- JDBC
- JavaBeans
- RMI
- 内部类
- 反射

## J2SE 1.2 （1998-12-08）
- 集合框架
- Java IDL（接口描述语言）支持CORBA（平台对象请求代理体系结构）
- JIT(Just In Time)编译器
- 数字签名
- 控制授权/访问系统资源的策略工具
- JFC(Java Foundation Classes)，包括Swing1.0，拖放和Java2D类库
- Java Plug-In（运行插件)
- JDBC中引入可滚动结果集，BLOB，CLOB，批量更新和用户自定义类型
- Applet中添加声音支持
- 字符串常量做内存映射

## J2SE 1.3 （2000-05-08）
- 数学运算
- Timer API
- Java Sound API
- CORBA IIOP实现RMI的通信协议
- Java 2D
- JAR文件索引

## J2SE 1.4 （2002-02-13）
### 语言增强
- 断言

### APIs
- XML解析器
- Java打印服务
- Logging API（日志功能）
- Java Web Start
- JDBC 3.0 API（jdbc高级)
- Preferences API
- 链式异常处理（try-catch-catch...）
- 引入Image I/O API （图片流)
- NIO（高级流）
- XSLT转换器
- 支持IPV6
- 支持正则表达式

## Java SE 5.0 （2004-09-30）
### 语言增强
- 泛型
- 增强for循环
- 自动装箱拆箱
- 枚举
- 可变参数
- 静态导入
- 注解

### JVM
- JMM
- Introspector 内省

### APIs
- concurrent

## Java SE 6 （2006-12-11）
### 语言增强
无

### APIs
- java.util.function包
- java.util.stream包
- java.awt新增Desktop类和SystemTray类
- 使用JAXB2来实现对象与XML之间的映射
- 轻量级 Http Server API
- 插入式注解处理API(lombok使用该特性来实现的)
- STAX，处理XML文档的API
- Compiler API
- 对脚本语言的支持（ruby, groovy, javascript）

## Java SE 7 （2011-07-28）
### 语言增强
- 整数类型能够用二进制来表示（前缀0b/0B）
- 数字常量支持下划线
- switch 支持String字符串类型
- 泛型实例化类型自动推断，即”<>”
- 改进可变参的警告和错误
- try-with-resources，资源自动关闭
- catch捕获多个异常类型，用（|）分隔开

### APIs
- 全新的NIO2.0 API
- Fork/join 并行执行任务的框架

## Java SE 8 （2014-03-18）
### 语言
- lambda 表达式和函数式接口
- 接口的默认方法
- 方法引用
- 重复注释
- 更好的类型推断
- 注解的扩展 （扩展了注解可以使用的范围，包括：局部变量，泛型，超类，接口实现，方法的exception声明等）

### 编译器
- 参数名字

### APIs
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
