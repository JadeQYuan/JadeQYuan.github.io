title: Linux基础
description: Linux基础
categories:
  - Linux
author: Jade
date: 2021-11-28 20:35:00
---

## 目录
- /bin 系统普通用户命令
- /sbin root命令
- /usr/bin 系统普通用户命令
- /usr/sbin root命令
- /etc 系统默认配置目录
- /root 
- /home 
- /lib 函数库
- /media 光盘
- /mnt U盘、硬盘
- /misc 磁带
- /proc 内存的过载点
- /sys 内存的过载点
- /temp 临时目录
- /usr 系统资源
- /var 系统可变文档
- /boot 启动目录

## 运行级别
- 0 关机
- 1 单用户模式
- 2 不完全的命令行
- 3 完全的命令行
- 4 系统保留
- 5 图形界面
- 6 重启

查看： run level
修改： init x
修改开始时级别： /etc/inittab

## 用户、用户组
### 文件
- /etc/group 存储当前系统中所有用户组信息 （组名称:组密码占位符:组编号:组中用户名列表）
- /etc/gshadow 存储当前系统中用户组的密码信息 （组名称:组密码:组管理者:组中用户列表）
- /etc/passwd 存储用户组中用户信息 （用户名:密码占位符:用户编号:用户组编号:用户注释信息:用户主目录:shell类型）
- /etc/shadow 存储用户密码信息 （用户:密码:......）

### 命令
- 添加用户组： groupadd 组名
- 修改用户组名称： groupmod -n 新组名 旧组名
- 修改用户组编号： groupmod -g 编号 组名
- 删除用户组：groupdel 组名
- 添加用户： useradd 用户名
- 修改用户： usermod -l 旧名 新名
- 删除用户： userdel 用户名
- 锁定： passwd 用户名 -l
- 解锁： passwd 用户名 -u
- 清除命令： passwd 用户名 -d

## 权限
```shell
chmod [选项] 模式 文件名
chown [组名:]用户名 文件名
chgrp 组名 文件名
```
-R 递归

## 压缩/解压缩
压缩文件格式： .zip、.gz、.bz2、.tar.gz、.tar.gz2
### tar
- -c 打包、-x 解压、 -t 查看
- -v 显示过程
- -f 指定打包后的文件名
- -z .tar.gz格式 -j .tar.bz2格式

### zip
- 压缩文件 zip *.zip *
- 压缩目录 zip -r *.zip 目录
- 解压缩 unzip 压缩文件

### gzip
- 压缩文件 gzip 源文件 （源文件消失）
- 压缩目录 gzip  -r 目录
- 解压 gunzip 压缩文件
- 解压 gzip -d 压缩文件

### bzip
- 压缩文件 bzip2 源文件
- 不能压缩目录
- 解压 bzip2 -d 压缩文件
- 解压 bunzip2 压缩文件

## 帮助命令
### map
- 查看级别 map -f 命令  ->  whatis 命令
- 查找  map -k 命令  ->  apropos 命令

### help

## ssh操作
- ctrl + L  清屏
- ctrl + c  强制退出
- ctrl + u  删除至行首
- ctrl + a  Home
- ctrl + e  End
- ctrl + r  在历史命令搜索
- ctrl + z  放入后台

## VI操作模式
visual interface
命令模式、输入模式、底行模式

- :w 保存
- :q 退出
- :! 强制执行
- :ls 列出当前打开文件
- :n 切换到下一个打开的文件
- :N 切换到上一个打开的文件
- :15 定位到15行
- /xxx 向后搜索
- ?xxx 向前搜索

## 常用命令
命令格式： 命令 [选项] [参数]
### pwd
print working directory
- ~ 当前用户家目录
- # 管理员用户
- $ 普通用户

### ls
- -a all
- -l long 文件类型（-、d、l、...）
- -d 目录属性
- -h human 人性化显示
- -i inode i结点

### mv
```shell
mv [原文件/目录] [目标文件/目录]
```

### 创建目录 mkdir 
- -p 递归创建

### 删除 rm 
- -f force 强制
- -r 删除目录

### 复制 cp
- -r 目录
- -p 连带文件属性复制
- -d 若源文件是链接文件，则复制链接属性

### 链接 ln 
ln [原文件] [目标文件]
-s 软链接

### 文件搜索 locate
```shell
locate 文件名
```

### 命令搜索
```shell
where is 命令
which 命令
```
where 查看命令所在位置-b 和帮助文档-m
which 查看命令所在位置和别名

### 字符串搜索 grep
```shell
grep [选项] 字符串 文件名
```
- -i 忽略大小写
- -v 取反

### 文件搜索 find
```shell
find [搜索目录] [搜索条件（通配符）]
```
- atime 文件访问时间
- ctime 改变文件属性时间
- mtime 改变内容时间
- -10 10天内修改
- +10 10天前修改
- 10 10天前当天修改
- -size 25k/+25k/-25k
- -inum
- -a and
- -o or

### 磁盘管理 
#### df
- -l 本地磁盘
- -a 所有文件系统
- -h 1024 进制换算
- -H 1000 进制换算
- -T 分区类型
- -t 显示指定类型
- -x 不显示指定类型

#### 挂载
```shell
mount ntfs-3g 目录 目录
umount 目录
```

#### 其它
- du 统计磁盘上的文件大小
  - -b -k -m
  - -h -H 
  - -s 指定统计目标
- fdish 添加MBR分区
- parted 添加GPT/MBR分区
- mkfs 格式化
