title: WSL2
categories:
  - Linux
description: WSL2
author: Jade
date: 2021-06-03 15:16:56
---
# WSL2
> How/Why


## WSL
一、 更新windows  
	wsl2需要： ×64架构 需要1903及更高 
	下载windows易升，从1909版本升级到20H2。

二、 启用windows功能
	适用于Linux的Windows子系统
	虚拟机平台  wsl2需要
	
三、 登录microsoft账号，加入windows预览体验计划    只是简化安装需要
	下载ubuntu，windows terminal
	
四、 wsl2
	下载linux内核更新包并运行
	设置默认版本为2





## 安装centos
1. 下载镜像 https://github.com/CentOS/sig-cloud-instance-images/tree/CentOS-8-x86_64
2. windows安装Chocolatey
3. 通过Chocolatey安装LxRunOffline
4. 通过LxRunOffline安装centos
	LxRunOffline.exe  install -n centos -d E:\WSL\CentOS -f  E:\WSL\centos-8-x86_64.tar.xz
		-n 名称
		-d 安装路径
		-f 文件路径
	启动： LxRunOffline run -n centos
5. 安装VcXsrc
	需要VcXsrc来显示
6. 安装图形界面
	yum install -y epel-release
	yum groupinstall -y "Xfce"
	重启
	export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}'):0.0
	startxfce4
	
	export DISPLAY=172.20.128.1:0.0
	
##  docker


## 步骤
1. LxRunOffline.exe  install -n c8 -d D:\WSL2\WSL_C8 -f  E:\down\centos-8-x86_64.tar.xz
2. yum install net-tools -y
3. yum -y install xorg-x11-xauth
4. yum -y install firefox ( libXcomposite libXcursor libXft libXi libXinerama libXrandr libXrender libXtst libXpm )
5. yum -y install mesa-libGL

yum -y install which


bat启动文件
.\config.xlaunch
start /min wsl -d c8 idea

## 安装
1. 安装jdk： yum install -y java-1.8.0-openjdk
2. 安装mysql: yum install -y mysql-server
3. 安装maven：下载、解压、设置环境变量
4. 安装node：yum install -y nodejs
5. 安装git：yum install -y git
6. 安装svn：

