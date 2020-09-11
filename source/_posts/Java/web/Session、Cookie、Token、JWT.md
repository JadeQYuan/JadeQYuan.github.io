title: Session、Cookie、Token、JWT
categories:
  - Java
  - web
tags:
  - How
description: Session、Cookie、Token、JWT
author: Jade
date: 2020-09-11 16:58:00
---


## Session
会话，在服务端保存用户信息。
### 填坑
- 服务器保存用户信息，导致session占据过多的内存。
- 网站采用集群部署，需要考虑session共享的问题。
- 多个应用共享session时，需要考虑蛞蝓问题。
- 如果交由cookie处理，需要考虑浏览器禁止cookie或不支持cookie的问题。

## Cookie
浏览器实现的一种数据存储功能。在客户端保存信息。

### 填坑
- 移动端对cookie支持不是很好。
- 容易被篡改，需要验证。
- 存储大小限制。
- 存储个数限制。
- 无法跨域。

## Cookie VS Session
- 安全性
- 存取值的类型
- 有效期
- 存储大小

## Token
令牌。
### 流程
1. 用户通过用户名密码

### 优点
- 无状态 （负载均衡器可以将请求转发到任意服务器）
- 可扩展 （可以扩展为第三方应用程序）
- 安全性 （可以蛞蝓）

### 填坑
- 需要加密。
- token传输方式。（header、payload、url）

## JWT
Json Web Token 是一个轻量级的认证规范，这个规范允许我们使用JWT在用户和服务器之间传递安全可靠的信息。其本质是一个token，是一种紧凑的URL安全方法，用于在网络通信的双方之间传递。
### 数据结构
Header.Payload.Signature
##### Header
JSON对象，描述JWT的元数据。
##### Payload
实际需要传递的数据。JWT官方规定了7个字段，供选用。

|name||desc|
|-|-|-|
|iss|issuer|签发人|
|exp|expiration time|过期时间|
|sub|subject|主题|
|aud|audience|受众|
|nbf|not before|生效时间|
|iat|issued at|签发时间|
|jti|jwt id|编号|
##### Signature
对前两部分的签名，防止数据篡改。

### 使用场景
对于SSO来说，每个系统都需要去CAS系统认证，如果使用jwt的话，可以通过算法来验签，而不需要通过数据库或者http接口验证。


<p style="text-align: center"><strong>END</strong></p>