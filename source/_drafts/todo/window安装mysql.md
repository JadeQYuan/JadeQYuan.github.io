	在window环境下， 安装mysql压缩版。
## 安装环境
- 操作系统： window10。
- mysql版本：mysql 8，压缩包安装。
## 安装过程
1. 解压mysql压缩包到安装位置。
2. 添加my.ini 配置文件，配置basrdir与datadir。
3. 切换目录，执行mysql初始化，初始化配置并查看临时密码
```
mysqld --initialize --console
```
4. 安装mysql
```
mysqld --install
```
5. 启动mysql服务
```
net start mysqld
```
6. 设置mysql root账号密码
```
mysql -u root -p
alter user 'root'@'localhost' identified with mysql_native_password by 'root';
```
7. 创建数据库，指定字符集
## 填坑
- 时区
	不设定时区使用操作系统的时区

***END***


