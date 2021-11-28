title: Linux软件安装
description: Linux软件安装
categories:
  - Linux
author: Jade
date: 2021-11-28 21:25:00
---

## 源码包安装
### 准备
- C语言编译器gcc
- 源码包 *.tar.gz

### 安装
1. 解压缩
2. 进入解压缩目录
3. ./config 软件配置与检查
4. make / make clean 编译
5. make install 编译安装
6. 启动

### 卸载
直接删除安装目录即可。

### 位置
- 源码保存位置 /usr/local/src/
- 安装位置 /usr/local

## RPM安装
### 命名规则
软件包名-版本-发布次数.适合平台.适合硬件平台.rpm

### 依赖
树依赖、环形依赖、库文件依赖/模块依赖

### 安装
rpm -ivh 包全名
-i install 安装
-e erase 卸载
-v verbose 显示详细信息
-h hase 显示进度

### 升级
rpm -uvh 包全名
-u upgrade 升级

### 卸载
rpm -e 包名
-e erase 卸载

### 校验
rpm -v 包名
-v validate 校验

### 查询命令
- -q query
- -a all
- -i information
- -p package
- -l list
- -f file

### 默认安装路径
rpm包安装位置由rpm包确定，可以指定perfix，但不建议。
/etc/ 配置文件
/usr/share/doc/ 软件使用手册
/usr/bin/ 可执行命令
/usr/shar/man/ 帮助文件
/usr/lib/ 程序所使用函数库

### 文件提取
rpm2cpio 包全名 | epio -idu 文件绝对路径

## yum在线安装
服务器使用最小化安装，用什么装什么，尽量不卸载。
### yum源文件
/etc/yum.repos.d/Centos-Base.repo
- [base]: 容器名称
- name: 容器说明
- mrrorlist: 镜像站点
- baseurl: yum源服务器地址
- enable: 是否生效，默认1，1生效，0无效
- gpgcheck: RPM数字证书，1生效，0无效
- gpgkey: 数字证书公钥文件保存位置

### 配置光盘yum源
1. 挂载光盘
2. 使默认失效，修改名字
3. 修改光盘配置yum源

### yum命令
- yum list
- yum search 关键字
- yum -y install 包名
- yum -y update 包名
- yum -y remove 包名
- yum grouplist
- yum groupinstall 软件组名
- yum groupremove 软件组名

## 脚本安装
eg nginx

## 比较
### 源码包
- 优点 开源，安装功能可配置，卸载方便，干净。
- 缺点 编译时间长，编译出错重复安装，安装步骤多。
### 二进制包
- 优点 安装、升级、查询、卸载简单，速度快。
- 缺点 不开源，不灵活，依赖性强。
### 脚本
- 优点 简单、迅速、方便。
- 缺点 软件版本、功能不能自定义。
