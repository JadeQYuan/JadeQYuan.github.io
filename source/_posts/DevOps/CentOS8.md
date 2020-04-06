---
title: CentOS8
date: 2020-02-05 11:04:49
categories:
  - DevOps
tags:
  - How
  - CentOS8
description: CentOS8安装过程，分区设置，以及在其上安装软件，包括docker，nginx，mysql，jenkins，git等。
---

> 最近centos 8发布，而且之前系统安装软件、文件路径都不太符合现在所理解的一些规范，所以准备重新安装系统。
## 系统安装
### 机器配置
- 型号： HP200 Pro G1 MT（(J1800)）
- 处理器： Intel Celeron J1800(2.41GHz/L3 1M)，双核双线程
- 内存： 4G DDR3 1600
- 硬盘： 500G机械硬盘

### 安装步骤
1. 阿里云下载centos8 iso镜像，制作U盘启动。
2. 开机时不插键盘，出现键盘找不到时，插入usb键盘，按esc，设置引导。
3. 选择最小安装，设置磁盘分区，开启网络配置，开始安装。

### 磁盘分区
|路径|格式|大小|
|-|-|-|
|/boot|-|512MB|
|/boot/efi|-|256MB|
|swap|-|8GB|
|/home|-|150GB|
|/var|-|50GB|
|/|-|260GB左右(剩余全部)|

### 填坑
- 主板键盘为ps/2接口，只能通过ps/2接口进入BIOS设置（ps/2转usb转换头也不行）。
> 开机时不插键盘，出现键盘找不到时，插入usb键盘，按esc。
- 镜像开机时选择install选项后不出现安装界面。
> 选择install选项，按e键进入编辑页面，将label设置为/dev/sdb4，按ctrl+X执行安装。
> PS1: 可以先修改为linux dd查看设备，确定之后在修改。
> PS2：在引导系统中，按Ctrl + Shift + Delete 组合键重启。
- 使用DVD镜像安装时，提示 Pane is DEAD，而使用虚拟机安装是没有问题的。
> 使用网络版镜像安装，在设置安装源时，先联网，然后选择从网络安装，设置镜像仓库地址。
> PS：网络版镜像应该不是官网的，而是阿里云提供的。

## 软件安装
### 规范
/usr/lcoal 安装系统软件
/opt 安装临时软件，存储安装包（压缩包安装方式）
/var 放日志文件

### 开放端口及服务
- 查看指定区域(public)所有开启的端口号/服务
```shell
firewall-cmd --zone=public --list-ports / --list-service
```
- 开放端口/服务（防火墙重启生效）
```shell
firewall-cmd --zone=public --add-port=80/tcp / --add-service=http --permanent
```
- 查看所有服务
```shell
 firewall-cmd --get-services
```

### docker
- 查看自带的，yum search docker 发现自带的不是我们想要的。
- 下载docker-ce repo
```shell
curl https://download.docker.com/linux/centos/docker-ce.repo -o /etc/yum.repos.d/docker-ce.repo
```
- 安装containerd.io依赖
```shell
yum -y install https://download.docker.com/linux/fedora/30/x86_64/stable/Packages/containerd.io-1.2.6-3.3.fc30.x86_64.rpm
```
- 安装docker
```shell
yum -y install docker-ce
```
- 设置开机启动
```shell
systemctl enable docker
```

### nginx
- 安装
```shell
yum install nginx
```
- 设置开机启动
```shell
systemctl enable nginx
```
- nginx配置文件路径：/etc/nginx/nginx.conf
- nginx日志文件路径：/var/nginx

### mysql
> 通过docker安装mysql服务，简单，省事。
> 但是docker容器具有临时性，而mysql的数据要持久化，所以通过docker启动MySQL，然后通过挂载卷的方式保存数据，是否是个好的选择呢？
- 拉取镜像
```shell
docker pull mysql:8
```
- 启动容器
	将容器设置为自动重启，这样服务器开机或docker服务重启时会自动启动容器。
	使用 -e 选项为mysql设置root账号密码。

```shell
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --restart=always --name mysql mysql:8
```
- 进入容器
```shell
docker exec -it mysql /bin/bash
```

### jenkins
> 使用docker安装jenkins，方便，省事。
- 拉取镜像
	使用latest版本
```shell
docker pull jenkinsci/blueocean
```
- 启动容器
```shell
docker run -u root -d -p 8080:8080 -v /var/jenkins_data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --restart=always --name jenkins jenkinsci/blueocean
```
- 获取admin默认密码
- 自定义安装插件
- 创建管理员用户密码

#### 填坑
1. 启动jenkins容器，配置nginx代理，静态资源访问不到
2. 开启防火墙，启动jenkins容器，开放8080端口，内网访问不到
3. 在2的前提下，关闭防火墙，内网可以访问，但是jenkins提示离线
4. 开机启动docker，firewalld，然后关闭防火墙，启动容器，启动不起来，提示： docker: Error response from daemon: driver failed programming external connectivity on endpoint jenkins (0a8069842c234eaae6d36192f62b5d9503926c0167cae15711300168103c5b1e):  (iptables failed: iptables --wait -t nat -A DOCKER -p tcp -d 0/0 --dport 8080 -j DNAT --to-destination 172.17.0.2:8080 ! -i docker0: iptables: No chain/target/match by that name.
5. 最终解决办法：开机启动docker，firewallld, 然后关闭防火墙，docker服务重启，然后启动容器，ok！（问题，怎么能不关闭防火墙）
PS: 每次防火墙重启时都需要重启docker服务。

### git
> github国内访问有点慢，有时候提交需要等好一会儿，而且自己的那点代码，感觉放在开源网站有点low，所以决定在自己服务器安装一个git服务器，等项目做的有点水平了，在放到github上去。
#### ssh版本
> Protocol 2

#### git协议选择
> 通过查看git官网文档，git有四种可选择的协议来传输资料，分别是local，git，ssh，http。
> 其中local是本地协议，不能通过网络访问，git协议缺乏授权机制。
> http协议安装比较复杂，等后期对相关知识更加了解在做。
> 暂时选择git协议，使用密钥的方式进行授权，添加访问用户时需要添加公钥到服务器。
#### 安装过程
1. 安装git软件
```shell
yum install git
```
2. 创建git用户
```shell
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
#### 创建git仓库
> 在git目录下新建.git结尾文件夹，进入文件夹，创建一个裸仓库。
```shell
git init --bare
```
#### 填坑
- git用户密码
> git用户不必设置密码，没有必要。
- 权限问题
> git用户根目录下的所有文件及目录都应该属于git用户，每次创建完git仓库时也要修改目录所属用户，否则会提示 无权限访问。
- 公钥
> 使用 >> 操作可以将公钥追加到文件里面。
> 使用 > 操作会清空文件的内容，并把新内容添加到文件里面。
- git clone
> 在使用 TortoistGit 进行git clone 的时候，需要勾选 Load Putty Key 选项，并选择私钥。
> 在使用 git bash clone的时候需要保证当前用户目录.ssh文件夹下面存在私钥。
- RSA
> RSAAuthentication 是对ssh 1版本的支持，在本环境中，使用ssh 2，所以没有这个配置，忽略即可。
> 如果自己手动加上了这个配置，在查看日志文件时会有警告。
- bare
> 裸仓库即不包含工作目录的仓库。

<p style="text-align: center"><strong>END</strong></p>
