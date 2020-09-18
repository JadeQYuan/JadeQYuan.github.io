title: netty
categories:
  - Java
  - 并发
tags:
  - How
  - ''
description: netty
author: Jade
date: 2020-09-18 16:25:00
---
## netty

## class
### EventLoopGroup
线程池，继承自 ScheduledExecutorService。  
用做服务器时有两个线程池，分别为接收连接线程池与工作线程池。用作客户端时有一个线程池。  
具体实现类有NioEventLoop、DefaultEventLoop、EpollEventloop。

### AbstractBootstrap
启动类。服务器启动类为ServerBootstrap，客户端启动类为Bootstrap。
#### group
指定线程池。
#### channel
指定通道，根据通道可以判断是服务器/客户端、TCP/UDP。
#### childHandle
指定消息的处理器。
#### option、childOption
通过常量指定TCP/UDP协议的相关配置。如backlog、keepalive等。
#### bind
绑定端口。

### Channel
netty的通道。

### ChannelFuture
继承自Future。

<p style="text-align: center"><strong>END</strong></p>