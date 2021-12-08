title: Java版本与特性
categories:
  - Java
description: Java版本与特性
author: Jade
date: 2020-07-21 16:39:00
---

Java是由Sun Microsystems公司（简称Sun公司）于1995年5月推出的Java程序设计语言和Java平台的总称。“Write Once, Run Anywhere”。
## 术语
- JDK: Java Development Kit，Java开发工具包，包括JVM、Java类库、Java工具。
- Java 平台: 用Java语言编写的软件运行的平台，包括SE、ME、EE。

## Java 发展史
- 1995-5-23，Oak语言更名为Java，并发布JDK 1.0α2和HotJava 浏览器（1999年停止发展）。10月，发布JDK 1.0β。
- 1996-1-23，JDK 1.0发布，Java语言第一个正式版本的运行环境。
- 1997-2-19，JDK 1.1发布。
- 1998-12-4，Java2平台拆为3个方向，J2SE 1.2（JDK 1.2）发布。
- 1999-4-27，HotSpot虚拟机发布。
- 1999-12-12, J2EE 1.2发布。
- 2000-5-8，J2SE 1.3（JDK 1.3）发布。
- 2001-9-24，J2EE 1.3发布。
- 2002-2-13，J2SE 1.4（JDK 1.4）发布。
- 2003-11-11，J2EE 1.4发布。
- 2004-9-30，J2SE 5.0（JDK 1.5）发布，修改版本号命名方式，1.x保留为内部命名方式。
- 2006-11-13，Sun在GPL许可证下开源Java。
- 2006-12-11，Java SE 6发布，使用Java SE替换J2SE，版本号去掉“.0”。
- 2006-5-11，Java EE 5发布。
- 2009-4-20，Oracle以74亿美元收购Sun。
- 2011-7-28，Java SE 7发布，LTS（2022-7）。
- 2013-5-28，Java EE 7发布。
- 2014-3-18，Java SE 8发布，LTS（2030-12）。
- 2017-8-31，Java EE 8发布。
- 2018-9-25，Java SE 11发布，LTS（2026-9）。
- 2019-9-10，Jakarta EE8发布，Java EE更名为Jakarta EE。
- 2020-11-22，Jakarta EE9发布。
- 2021-9-17，Java SE 17发布，从此免费提供，LTS（2029-9）。

## Java/JDK 新特性
### Java SE 11
- String API isBlank、strip、stripTrailing、stripLeading、repeat、lines.count
- Optinal API isEmpty...
- 局部变量类型推断加强 var上可以加注解
- HttpClient
- 垃圾回收ZGC

### Java SE 10
- 局部变量类型推断
- 不可变集合的改进
- 并行全垃圾回收器 G1
- 线程本地握手
- Optional新增orElseThrow()方法
- 类数据共享
- Unicode 语言标签扩展
- 根证书

### Java SE 9
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

### Java SE 8
#### 语言
- lambda 表达式和函数式接口
- 接口的默认方法和静态方法
- 方法引用
- 重复注释
- 更好的类型推断
- 注解的扩展 （扩展了注解可以使用的范围，包括：局部变量，泛型，超类，接口实现，方法的exception声明等）

#### 编译器
- 参数名字

#### JDK
- Optional
- Stream
- 时间日期API
- Nashorn javascript引擎
- Base64
- 并行数组 （增加了支持并行的数组处理）
- 并发 （新增StampedLock、DoubleAccumulator、DoubleAdder、LongAccumulator、LongAdder等）

#### 工具
- Nashorn引擎 jjs
- 类依赖分析工具 jdeps

#### JVM
- JVM内存永久区被metaspace替换，JVM参数 -XX:PermSize 和 -XX:MaxPermSize 被 -XX:MetaSpaceSize 和 -XX:MaxMetaSpaceSize 代替。

### JDK 1.7
- switch 支持String字符串类型
- try-with-resources，资源自动关闭
- 整数类型能够用二进制来表示
- 数字常量支持下划线
- 泛型实例化类型自动推断,即”<>”
- catch捕获多个异常类型，用（|）分隔开
- 全新的NIO2.0 API
- Fork/join 并行执行任务的框架

### JDK 1.6
- java.awt新增Desktop类和SystemTray类
- 使用JAXB2来实现对象与XML之间的映射
- 轻量级 Http Server API
- 插入式注解处理API(lombok使用该特性来实现的)
- STAX，处理XML文档的API
- Compiler API
- 对脚本语言的支持（ruby, groovy, javascript）

### JDK 1.5
- 自动装箱拆箱
- 泛型
- 元数据
- Introspector 内省
- 枚举
- 静态引入
- 可变长参数
- foreach
- JMM
- concurrent

### JDK 1.4
- XML解析器
- Java打印服务
- Logging API（日志功能）
- Java Web Start
- JDBC 3.0 API（jdbc高级)
- 断言
- Preferences API
- 链式异常处理
- 支持IPV6
- 支持正则表达式
- 引入Imgae I/O API （图片流);
- NIO（高级流）
- XSLT转换器

### JDK 1.3
- 数学运算
- Timer API
- Java Sound API
- CORBA IIOP实现RMI的通信协议
- Java 2D
- JAR文件索引

### JDK 1.2
- J2SE/J2EE/J2ME
- EJB
- Java IDL（平台对象请求代理体系结构）
- 集合框架
- JIT(Just In Time)编译器
- 数字签名
- JFC(Java Foundation Classes), 包括Swing1.0, 拖放和Java2D类库
- Java Plug-In（运行插件)
- JDBC中引入可滚动结果集,BLOB,CLOB,批量更新和用户自定义类型
- Applet中添加声音支持
- 字符串常量做内存映射
- 控制授权/访问系统资源的策略工具

### JDK 1.1
- JAR
- JDBC
- JavaBeans
- RMI
- Inner Class
- Reflection

### JDK 1.0
- Classic VM（虚拟机）
- Applet（java小应用程序）
- AWT（java图形设计）
