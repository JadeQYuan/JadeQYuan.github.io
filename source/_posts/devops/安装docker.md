---
title: 安装docker
date: 2020-02-05 11:04:49
categorys: 
  - DevOps
tags: 
  - How
  - docker
---

	记录服务器安装软件过程。
## 规范
/usr/lcoal 安装系统软件
/opt 安装临时软件，存储安装包（压缩包安装方式）
/var 放日志文件

## docker
- 查看自带的，yum search docker 发现自带的不是我们想要的。
- 下载docker-ce repo
```
curl https://download.docker.com/linux/centos/docker-ce.repo -o /etc/yum.repos.d/docker-ce.repo
```
- 安装containerd.io依赖
```
yum -y install https://download.docker.com/linux/fedora/30/x86_64/stable/Packages/containerd.io-1.2.6-3.3.fc30.x86_64.rpm
```
- 安装docker
```
yum -y install docker-ce
```
- 设置开机启动
```
systemctl enable docker
```
## nginx
- 安装
```
yum install nginx
```
- 设置开机启动
```
systemctl enable nginx
```
- nginx配置文件路径：/etc/nginx/nginx.conf
- nginx日志文件路径：/var/nginx
## 开放端口及服务
- 查看指定区域(public)所有开启的端口号/服务
```
firewall-cmd --zone=public --list-ports / --list-service
```
- 开放端口/服务（防火墙重启生效）
```
firewall-cmd --zone=public --add-port=80/tcp / --add-service=http --permanent
```
- 查看所有服务
```
 firewall-cmd --get-services
```

	通过docker安装mysql服务，简单，省事。
	但是docker容器具有临时性，而mysql的数据要持久化，所以通过docker启动MySQL，然后通过挂载卷的方式保存数据，是否是个好的选择呢？
## 安装步骤
- 拉取镜像
```
docker pull mysql:8
```
- 启动容器
	将容器设置为自动重启，这样服务器开机或docker服务重启时会自动启动容器。
	使用 -e 选项为mysql设置root账号密码。

```
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --restart=always --name mysql mysql:8
```
- 进入容器
```
docker exec -it mysql /bin/bash
```
- 创建数据库
```
create database database_name DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
```
- 创建表


	使用docker安装jenkins，方便，省事。
## 安装过程
- 拉取镜像
	使用latest版本
```
docker pull jenkinsci/blueocean
```
- 启动容器
```
docker run -u root -d -p 8080:8080 -v /var/jenkins_data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --restart=always --name jenkins jenkinsci/blueocean
```
- 获取admin默认密码
- 自定义安装插件
- 创建管理员用户密码
	knoiwng/...
## 填坑
1. 启动jenkins容器，配置nginx代理，静态资源访问不到
2. 开启防火墙，启动jenkins容器，开放8080端口，内网访问不到
3. 在2的前提下，关闭防火墙，内网可以访问，但是jenkins提示离线
4. 开机启动docker，firewalld，然后关闭防火墙，启动容器，启动不起来，提示： docker: Error response from daemon: driver failed programming external connectivity on endpoint jenkins (0a8069842c234eaae6d36192f62b5d9503926c0167cae15711300168103c5b1e):  (iptables failed: iptables --wait -t nat -A DOCKER -p tcp -d 0/0 --dport 8080 -j DNAT --to-destination 172.17.0.2:8080 ! -i docker0: iptables: No chain/target/match by that name.
5. 最终解决办法：开机启动docker，firewallld, 然后关闭防火墙，docker服务重启，然后启动容器，ok！（问题，怎么能不关闭防火墙）
PS: 每次防火墙重启时都需要重启docker服务。


***END***
