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

## JDK 1.0
## JDK 1.1
## JDK 1.2
...


## jdk9
1. 模块化
2. jShell
3. 接口可定义private方法 （只能在接口内部调用）
4. try with resource 优化
5. String, StringBuilder, StringBuffer 中的value由char[]改为byte[]
6. List、Set、Map 添加of方法创建只读集合
7. InputStream流加强
8. StreamAPI takeWhile、dropWhile、ofNullable、iterate
9. Optional增加stream()
10. 垃圾回收机制

## jdk10
1. 局部变量类型推断 var
2. 只读集合 copyOf

## jdk11
1. String API isBlank、strip、stripTrailing、stripLeading、repeat、lines.count
2. Optinal API isEmpty...
3. 局部变量类型推断加强 var上可以加注解
4. HttpClient
5. 垃圾回收ZGC
