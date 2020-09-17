title: synchronized
categories:
  - Java
  - 并发
tags:
  - How
description: synchronized
author: Jade
date: 2020-09-17 17:09:00
---

## synchronized使用及编译
### 方法
编译时添加ACC_SYNCHRONIZED标记。
### 代码块
默认添加try-finally，编译生成一条monitorenter指令和两条monitorexit指令。
### 总结
如果synchronized作用的对象是非静态方法或者对象，则它取得锁是对象锁；如果synchronized作用的对象是静态方法或者类，则它取得的锁是类锁。类锁与对象锁是两把不同的锁。

## 锁
重量级锁依赖于系统的同步函数，在linux上使用mutex互斥锁，最底层实现依赖于futex。这些同步函数都涉及到用户态和内核态的切换，进程的上下文切换，成本较高。
### 对象头
在JVM中，对象在内存中除了本身的数据外还会有对象头，对于普通对象而言，其对象头有两类信息：mark word和类型指针，对于数据而言含会有一份记录数据长度的数据。  
类型指针是指向该对象所属类对象的指针。mark word用于存储对象的HashCode、GC分代年龄、锁状态等信息，在32位系统中位32字节，64位系统中为64字节。  
Java中任意对象都可以用作锁，锁信息可以存在对象头中。  
mark word中存储数据根据锁类型改变，当对象为无状态锁时，存储hashCode，当对象为偏向锁时，存储线程id，当对象为轻量级锁时，存储线程栈中Lock Record的指针，当对象为重量级锁时，存储堆中的monitor对象的指针。

### 重量级锁
传统意义上的锁，利用操作系统底层的同步机制实现Java中的线程同步。
### 轻量级锁
在运行时，同步块中的代码不存在竞争，不同的线程交替执行同步块中的代码。
### 偏向锁
在运行时，只有一个线程会调用相关同步方法。



<p style="text-align: center"><strong>END</strong></p>