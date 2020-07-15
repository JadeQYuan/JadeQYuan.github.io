title: Hexo搭建博客
categories:
  - 元
tags:
  - How
  - Hexo
description: 记录使用hexo搭建博客的过程，包括对于GitHub Pages的了解，对Jekyll与Hexo的使用对比，及hexo的搭建步骤，配置内容，页面生成等。
date: 2020-03-28 22:22:00
---

# GitHub Pages
> GitHub Pages 允许开发者自定义项目的首页，代替直接展示代码的方式。
## Jekyll
> GitHub Pages 默认的静态网站生成工具，通过项目中的相应的配置文件，可以自动打包部署。
## Hexo
> 静态网站生成工具，可以通过配置使GitHub支持。
## Jekyll VS Hexo
- 本地开发预览
> Jekyll 需要搭建完整的Ruby环境。
> Hexo 需要搭建NodeJS环境。
- 迁移
> GitHub Pages中对Jekyll的支持，使得我们太多去关心Jekyll的配置以及插件，这会在迁移过程中造成一定的影响。因为不知道配置是什么，及使用了哪些插件。
> Hexo的配置是自定义的。  
## Gitee
> 由于GitHub访问速度问题，也可使用Gitee Pages功能，其概念和GitHub概念相似。  
### GitHub Pages VS Gitee Pages
> Gitee 支持Jekyll、Hexo、Hugo，GitHub只支持Jekyll。 
> GitHub 支持自动打包部署，检测到代码提交时执行。Gitee个人免费版不知道自动打包部署，需要手动进行。
> GitHub 支持自定义域名。Gitee个人免费版不支持。
> GitHub 只支持master、gh-pages分支，当使用根路径访问时只支持master分支。Gitee支持任意分支。
## 自动打包部署
> 对于支持自动打包部署的情况，只需要提交源码到对应的分支就行，会自动打包并部署。
> 而不支持自动打包部署的情况，需要在本地通过命令生成部署到对应的分支。而将源码提交到另一个分支。

# Hexo 搭建过程
## 搭建步骤
> hexo init命令需要空文件夹，git clone会生成一个不为空的文件夹，所以创建过程中需要按以下步骤进行。
1. 初始化hexo项目
```shell
npx hexo init <dir name>
```
PS: 如不指定目录名称，则在当前文件夹下初始化，要求该文件夹为空。
2. 初始化git仓库
```shell
git init
```
3. 关联远程仓库
```shell
git remote add origin <url>
```

## 站点配置
> 项目目录下的_config.yml为站点配置文件，themes/?/_config.yml为主题配置文件。将主题文件复制到source/_data/next.yml进行修改。
1. 网站配置
其中 language为主题要求的值。
```yaml
title: <title>
subtitle: <subtitle>
description: <description>
keywords: <keywords>
author: <author>
language: zh-CN
timezone: Asia/shanghai
```
2. URL 配置
```yaml
url: <url>
root: /
permalink: :year:month/:category/:post_title/
```
3. 发布配置
可配置多个
```yaml
deploy:
- type: git
  repo: <url>
  branch: master
```
4. 主题配置
使用最新NexT主题
```shell script
git clone https://github.com/theme-next/hexo-theme-next themes/next
```
```yaml
theme: next
```
5. CNAME配置
如需自定义域名，且手动打包部署，则CNAME配置应跳过渲染。相对路径为source。
```yaml
skip_render: CNAME
```

## 主题配置
1. 菜单配置
```yaml
menu:
  home: / || fa fa-home
  about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
```
2. 样式配置
```yaml
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```
3. pjax配置
页面局部刷新功能
```yaml
pjax: true
```
添加依赖
```shell
git clone https://github.com/theme-next/theme-next-pjax themes/next/source/lib/pjax
```
4. 其他配置
每个配置的地方都有注释说明。
- 图标 favicon
- 头像 avatar
- 代码高亮样式 highlight_theme
- 局部页面刷新 pjax
- 中英文之间空格 pangu
- 阅读进度条 reading_progress
- github_banner
- 书签 bookmark
- 评论 gitalk
- 公式 math
- 搜索 search
- RSS
- 捐赠 reward

# 文章与页面
1. 新建文章
```shell
hexo new [layout] <title>
```
layout为scaffolds中定义的模板，默认为post
2. 新建页面
```shell
hexo new page archives/categories/tags/about
```
在各自index.md中修改其type为主题菜单配置中名称，除about外，其它都不需要编辑。
3. 搜索页面
```shell
npm install hexo-gengerator-searchdb
```
站点配置中新增
```yaml
search:
    path: search.xml
    field: post
    format: html
    limit: 10000
```
主题配置
```yaml
local_search:
  enable: true
  trigger: auto
  top_n_per_article: 5
  unescape: false
  preload: false
```
4. 404页面

***END***
