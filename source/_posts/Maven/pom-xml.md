title: pom.xml
categories:
  - Maven
description: pom.xml
author: Jade
date: 2021-06-24 17:16:00
---


## dependencyManagemet与dependency
dependencyManagemet 只是管理版本，并不下载依赖
dependency 添加依赖

## pachaging 默认jar，可选jar、pom、war
- jar 调用或者作为服务
- pom 一般为父子继承使用
- war web项目

## spring-boot-parent 与 spring-boot-dependency
- 风格不同，功能一样
- 如果有自己的parent，则无法使用spring-boot-parent，只能使用spring-boot-dependency方式
- 使用spring-boot-parent需要配置 <relativePath/>
- 使用spirng-boot-dependency 需要配置 scope=import、type=pom
