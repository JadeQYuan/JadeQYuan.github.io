title: Java平台
categories:
  - Java
  - Java平台
description: Java平台
author: Jade
date: 2020-07-21 16:39:00
---

Java是由Sun Microsystems公司（简称Sun公司）于1995年5月推出的Java程序设计语言和Java平台的总称。“Write Once, Run Anywhere”。

## 术语
- Java 平台：用Java语言编写的软件运行的平台，包括SE、ME、EE。JavaSE有两个实现产品：JDK、JRE。
- JDK：Java Development Kit，Java开发工具包，包括JVM、Java类库、Java工具。
- JRE：Java Runtime Environment，Java运行时环境。

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

## Open JDK
Sun在JavaOne 2006中宣布将成为开源软件，并建立了Open JDK社区。
2006-11-13，Sun根据GNU通用公共许可证将Java HotSpot虚拟机和编译器作为免费软件发布。
2007-5-8，Sun在GPL下发布了Java类库的完整源代码。

OpenJDK是Java 平台标准版 (Java SE) 的免费开源实现。
OpenJDK是由OpenJDK Community 、Oracle、IBM 领导，连同 Alibaba，Amazon，Ampere，Azul，BellSoft，Canonical，Fujitsu，Google，Huawei，Intel，Java Community，JetBrains，London Java Community，Microsoft，Red Hat，SAP，SouJava，SUSE，Tencent，Twitter ，VMWare等第三方共同开发、维护的 JavaSE开源参考实现。

自 Java SE7开始往后的版本，所有的JDK都源自于Open JDK。
OpenJDK Community领导的OpenJDK Project是Java SE的官方参考实现，只产生OpenJDK源码，并不提供可以直接使用的二进制文件格式。现在能直接使用的二进制文件格式的 JDK都是被编译之后的程序。
OpenJDK官网指向的可下载二进制文件的地址，实际是 Oracle’s OpenJDK builds下载的地址。

## Java名称及版本
Java在5的时候改名，但内部还是使用1.x作为版本号。直到9。
Java1.x版本用在以下情况：

- java -version
- java -fullversion
- javac -source XX
- java.version System property
- java.vm.version System property
- @since XX
- JDK安装目录
- JRE安装目录

## Java平台概念图

![upload successful](/images/pasted-8.png)

JDK版本新特性主要包括JVM、Java SE API、工具及其API、语言特性。
其中Java SE API指java及javax包的更新，语言特性指编码方式。
