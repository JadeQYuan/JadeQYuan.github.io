title: maven
categories:
  - Maven
description: maven
author: Jade
date: 2020-07-14 14:11:00
---
  
## maven
版本管理工具。

## 生命周期
- clean
- default
  - validate
  - compile
  - package
  - install
  - deploy
- site

## pom.xml配置标签

## project
pom（project object model）文件根标签。

## modelVersion
声明pom文件project描述的版本。

## name、url、description
用于生成maven文档（mvn site）。

### maven.compile.source/target
对应javac指令的-source、-target参数。

### modules
在父模块打包时可将所有子模块进行打包，如果没有子模块，只打包当前目录。

### parent
实现继承，可以继承父模块properties、dependencies、dependencyManagement、...

#### relativePath
指定查找父模块的路径。
默认情况下，从当前pom.xml的上级目录查找， 为空值时从仓库查找。

### modules 与 parent
modules的功能是打包，parent的功能是继承。两者没有关系。即modules的子模块的parent可以是任意模块。

### dependencyManagement与dependency
dependencyManagement 只是管理版本，并不下载依赖
dependency 添加依赖

#### scope
- import
- provided
- compile
- runtime

#### type
pom，表示全部引入其它packing类型为pom的内容。与scope=import配合使用。

### packing 默认jar，可选jar、pom、war
- jar 调用或者作为服务
- pom 一般为父子继承使用
- war web项目

### plugins
maven是插件驱动的工具。插件是核心。

