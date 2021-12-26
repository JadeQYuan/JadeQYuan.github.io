title: io
categories:
  - Java
description: io
author: Jade
date: 2020-09-17 16:29:00
---

## 按流向
#### 输入流
以自己为参照，从外面读取为输入。
#### 输出流
以自己为参照，向外面写为输出。

## 按最小数据单元
#### 字节流
以8位（8bit即1byte）作为一个数据单元。
##### 字符流
以16位（16bit即2byte）作为一个数据单元。  
Java中的字符是Unicode编码，一个字符占用两个字节。
## 按功能
#### 节点流
可以
- 文件流
- 数组流
- 字符串流
- 管道流
#### 处理流
对一个已存在的流的连接和封装，通过对数据的处理为程序提供更为强大的读写功能。
- 缓冲流
- 转换流： 字节转字符，流中数据上全是字节。
- 数据流


- getResourceAsStream
    1. Class.getResourceAsStream(String)
        - 相对路径：当前类路径下
        - 绝对路径：classpath路径下
    2. Class.getClassLoader.getResourceAsStream(String)
       相对路径，不能是绝对路径
    3. ServletContext.getResourceAsStream(String)
       resource目录下，相对/绝对都一样