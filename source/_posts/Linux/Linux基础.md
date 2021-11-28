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

