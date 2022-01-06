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
maven有三套相互独立的声明周期。
不论要执行生命周期的哪一个阶段，都是从这个生命周期的开始执行。

### Clean Lifecycle
- pre-clean
- clean
- post-clean

### Default Lifecycle
- validate
- generate-sources
- process-sources
- generate-resources
- process-resources
- compile
- process-classed
- generate-test-sources
- process-test-sources
- generate-test-resources
- process-test-resources
- test-compile
- process-test-classed
- test
- prepare-package
- package
- pre-integration-test
- integration-test
- verify
- install
- deploy

### Site Lifecycle
- pre-site
- site
- post-site
- site-deploy

## pom配置
pom（project object model）文件是maven的配置文件。设置所有构建的配置。
project标签是根标签。
modelVersion标签声明pom文件project描述的版本。

## pom配置：描述
name、url、description 用于生成maven文档（mvn site）。

## pom配置：常用property
### maven.compile.source/target/release
对应javac指令的-source、-target参数。

### project.build.sourceEncoding/project.reporting.outputEncoding


## pom配置：坐标
groupId、artifactId、version。
仓库jar包路径：\[groupId\]/\[artifactId\]/\[version\]/\[artifactId\]-\[version\].jar。

## pom配置：继承与子模块
### modules
在父模块打包时可将所有子模块进行打包，如果没有子模块，只打包当前目录。

### parent
实现继承，可以继承父模块properties、dependencies、dependencyManagement、...

#### relativePath
指定查找父模块的路径。
默认情况下，从当前pom.xml的上级目录查找， 为空值时从仓库查找。

### modules 与 parent
modules的功能是打包，parent的功能是继承。两者没有关系。即modules的子模块的parent可以是任意模块。

## pom配置：依赖与依赖声明
### dependencyManagement与dependency
dependencyManagement 只是管理版本，并不下载依赖。
dependency 添加依赖。

#### scope
- compile 默认值
- provided 只在编译器提供，打包的时候过滤，
- runtime 强制面向接口编程，不能引入该包的类。
- test 编译器与测试阶段，打包的时候过滤。
- import 只在dependencyManagement标签且type=pom时有用，会用目标pom的dependencyManagement里的内容替换该依赖。
- system 类似provided，但需要显式提供jar路径（systemPath标签），不会在repository中查找。

#### type
pom，表示全部引入其它packing类型为pom的内容。与scope=import配合使用。

## pom配置：依赖传递
- 非compile范围的依赖不能传递。
- 路径最短者优先原则。
- 路径相同声明优先原则。
- optional=true显式声明不传递依赖。
- exclusions显式声明过滤依赖。

## pom配置：打包方式
packing 默认jar，可选jar、pom、war。
- jar 调用或者作为服务
- pom 一般为父子继承使用
- war web项目

## pom配置：不同环境
profile标签。

## pom配置：plugins
maven是插件驱动的工具。插件是核心。

