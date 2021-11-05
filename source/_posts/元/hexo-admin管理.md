title: Hexo admin后台管理
categories:
  - 元
description: 添加hexo-admin作为hexo的管理页面。
author: Jade
date: 2020-07-15 14:48:00
---

> 使用hexo搭建博客之后，通过在编辑器里面来记录文章总归不是一个好的方式，而hexo admin提供了后台管理的页面来通过页面管理文章。

## 安装
```
npm install hexo-admin
```
安装好之后会在根目录下生成一个配置文件，该配置文件可以保存页面settings中的配置。

## 发布  
管理页面中deploy功能需要添加配置。
1. 在_config.yml 中添加amdin发布命令的脚本路径。
2. 创建脚本文件。

PS: 该功能没有实现 


## 线上
github Pages是静态网站，不支持。支持其它动态的服务器。

## 图片
hexo admin 可以在编辑器内复制图片，图片将保存在images文件夹下，可自定义。
windows复制的图片需要去掉\...\。

## 其它
1. Posts页面没有分类，所有文章放在一起，看起来比较乱。
2. 新建文章能否按照分类按文件夹存放。
3. 添加分类和标签时只能输入，不能选择。
4. 不能编辑文章的描述，该描述影响列表页面的内容。

PS：  
（1）. 可以在文章编辑界面上方修改文章路径。  
（2）. 可以在_config.yml中添加 metadata - description 支持。

