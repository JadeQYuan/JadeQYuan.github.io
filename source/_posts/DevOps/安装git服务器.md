---
title: 安装git服务器
date: 2020-02-05 11:04:49
categorys: 
  - DevOps
tags: 
  - How
  - git
  - CentOS8
description: CentOS8过程，磁盘分区，机器配置等。
---

	github国内访问有点慢，有时候提交需要等好一会儿，而且自己的那点代码，感觉放在开源网站有点low，所以决定在自己服务器安装一个git服务器，等项目做的有点水平了，在放到github上去。
## 安装环境
- 操作系统
	CentOS 8
- ssh版本
	Protocol 2

## git协议选择
	通过查看git官网文档，git有四种可选择的协议来传输资料，分别是local，git，ssh，http。
	其中local是本地协议，不能通过网络访问，git协议缺乏授权机制。
	http协议安装比较复杂，等后期对相关知识更加了解在做。
	暂时选择git协议，使用密钥的方式进行授权，添加访问用户时需要添加公钥到服务器。
## 安装过程
1. 安装git软件
	``` 
	yum install git
	```
2. 创建git用户
	```
	adduser git (不用设置密码)
	```
3. 在git根目录下创建.ssh文件夹
4. 在git/.ssh目录下创建 authorized_keys 文件，用来存放用户公钥。
5. 设置git目录所属用户为git，.ssh目录权限为700，authorized_keys 文件权限为600。
6. 限制git账号使用ssh连接。
	git-shell: 登录成功后自动退出的shell
	查看git-shell命令路径： where is git-shell
	修改/etc/passwd中 git账号登录后的shell为git-shell全路径
7. 打开RSA认证。
	修改配置文件/etc/ssh/sshd_config 中 设置
	RSAAuthentication yes(centos 7.4 已弃用，忽略不设置)
	PubkeyAuthentication yes
	AuthorizedKeysFile .ssh/authorized_keys
## 创建git仓库
	在git目录下新建.git结尾文件夹，进入文件夹，创建一个裸仓库。
```
	git init --bare
```
## 填坑
#### git用户密码
	git用户不必设置密码，没有必要。
#### 权限问题
	git用户根目录下的所有文件及目录都应该属于git用户，每次创建完git仓库时也要修改目录所属用户，否则会提示 无权限访问。
#### 公钥
	使用 >> 操作可以将公钥追加到文件里面。
	使用 > 操作会清空文件的内容，并把新内容添加到文件里面。
#### git clone
	在使用 TortoistGit 进行git clone 的时候，需要勾选 Load Putty Key 选项，并选择私钥。
	在使用 git bash clone的时候需要保证当前用户目录.ssh文件夹下面存在私钥。
#### RSA
	RSAAuthentication 是对ssh 1版本的支持，在本环境中，使用ssh 2，所以没有这个配置，忽略即可。
	如果自己手动加上了这个配置，在查看日志文件时会有警告。
#### bare
	裸仓库即不包含工作目录的仓库。

<p style="text-align: center"><strong>END</strong></p>
