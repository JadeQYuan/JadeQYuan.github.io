title: volatile
categories:
  - Java
  - 并发
tags:
  - How
description: volatile 关键字
author: Jade
date: 2020-07-23 14:55:00
---

## 特性
- 保证了所有线程对这个变量操作时的可见性。
- 禁止指令重排序。  
PS: volatile只能保证对单次读/写的原子性，像i++属于复杂指令。

## 实现
- 读 当读一个volatile变量时，会将本地内存的值置为无效，直接从主内存中读取。
- 写 当写一个volatile变量时，JMM会把本地变量的值刷新到主内存。

## 实现原理
指令屏障。


<p style="text-align: center"><strong>END</strong></p>