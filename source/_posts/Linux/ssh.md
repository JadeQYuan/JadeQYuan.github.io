title: ssh
categories:
  - Linux
description: ssh
author: Jade
date: 2020-02-05 11:04:00
---


SSH （ Secure Shell ），建立在应用层基础上的安全协议

SCP（Secure Copy）、SFTP（SSH File Transfer Protocol）是基于ssh的协议，使用了ssh的加密功能

使用ssh-copy-id命令将公钥复制到远程主机。ssh-copy-id会将公钥写到远程主机的 ~/ .ssh/authorized_key 文件中

SSH之所以能够保证安全，原因在于它采用了非对称加密技术(RSA)加密了所有传输的数据。
从客户端来看，SSH提供两种级别的安全验证。
第一种级别（基于口令的安全验证）
第二种级别（基于密匙的安全验证）
