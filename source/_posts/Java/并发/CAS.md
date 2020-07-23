title: CAS
categories:
  - Java
  - 并发
tags:
  - How/Why
description: CAS
author: Jade
date: 2020-07-23 16:13:00
---

## CAS
Compare And Swap。

## 算法
CAS是一种无锁算法，CAS有3个操作数，主内存值V，工作内存值A，要修改的新值B。当且仅当A和V相同时，将主内存值V改为B，否则什么都不做。  
valueOffset: 主内存地址的偏移量。  
value：使用volatile关键字保证可见性。

## 问题
- ABA问题。JDK1.5提供了AtomicStampedReference类来解决，纪录值的版本。
- 循环时间长开销大。长时间不成功会一直自旋。
- 只能保证一个共享变量的原子操作。JDK1.5提供了AtomicReference类来保证引用对象之间的原子性，可以把多个变量放在一个对象里进行CAS操作。


<p style="text-align: center"><strong>END</strong></p>