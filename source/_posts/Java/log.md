title: log
categories:
  - Java
description: log
author: Jade
date: 2021-09-03 15:09:00
---


1. log path的配置，一般只输出指定路径的日志，那mybatis的日志和启动时打印的日志为什么不在此列
2. 判断当前日志是否可用？？？

1. 日志Facade
	jcl commons-logging (已停止更新)
		默认使用log4j的实现，找不到则使用jul的实现。
	slf4j (simple log facade for java)
2. 日志实现
	jul (java.util.logging jdk1.4 开始提供)
	log4j
	logback
		logback-core
		logback-classic
		logback-access
	log4j2
		log4j-api
		log4j-core
3. 集成使用
	部分集成使用需要添加额外适配包
	1. jcl+log4j2
		log4j-jcl
	2. jcl+logback
		jcl-over-slf4j
	3. slf4j+jul
		slf4j-jdk14
	4. slf4j+log4j
		slf4j-log4j12
	5. slf4j+log4j2
		log4j-slf4j-impl
