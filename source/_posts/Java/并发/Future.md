title: Future
categories:
  - Java
  - 并发
description: Future
author: Jade
date: 2020-09-10 14:23:00
---
## Future
非阻塞模型。
### 类图

![upload successful](/images/pasted-6.png)

### RunnableFuture
同时继承接口Runnable和Future。

### SchedualedFuture
延时、定时执行。

### ForkJoinFuture
可被拆分、合并。

### CompletableFuture
可以被显式完成。  

## FutureTask
### 状态
- NEW
- COMPLETING
- NORMAL
- EXCEPTIONAL
- CANCELLED
- INTERRUPTING
- INTERRUPTED

### 状态转换
NEW -> COMPLETING -> NORMAL
NEW -> COMPLETING -> EXCEPTIONAL
NEW -> CANCELLED
NEW -> INTERRUPTING -> INTERRUPTED

