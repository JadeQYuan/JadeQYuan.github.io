title: Executor
categories:
  - Java
  - 并发
tags:
  - How
description: Executor
author: Jade
date: 2020-09-10 13:16:00
---

## 线程池
Java5引入，用于控制线程的启动、执行和关闭。  
基于生产者-消费者模式实现。

## Executor
### Executor
接口，定义了线程池执行的方法，接收Runnale作为参数，无放回值。
### ExecutorService
ExecutorService的子类接口，定义了线程池的生命周期。定义了submit方法，返回Future对象。及其它方法。
### AbstractExecutorService
ExecutorService 的抽象实现类，对ExecutorService中定义的方法做了默认的实现。
### Executors
工具类，提供了一些常用的线程池，常用的线程池创建线程的工厂类。
### Pool
#### ThreadPoolExecutor
常用的线程池，继承自AbastractExecutorService
#### ScheduledThreadPoolExecutor
可定时、周期执行的线程池，继承自ThreadPoolExecutor
#### ForkJoinPool
可完成拆分合并的线程池，继承自AbstractExecutorService

## Executor VS Thread
- 性能
- 同一管理，线程间竞争
- 扩展性

## BlockingQueue
阻塞队列
### SynchronousQueue
直接提交任务，而不保持。
### LinkedBlockingQueue
无界队列，可以对无限多的任务排队
### DelayQueue
延时队列，延时提交
### ArrayBlockingQueue
有界队列，可以指定队列的长度。

## 创建线程池
ThreadPoolExecutor是最常用的线程池，该线程池创建需要以下参数。 

|参数|类型|说明|
|-|-|-|
|corePoolSize|int|核心线程数|
|maximumPoolSize|int|最大线程数|
|keepAliveTime|long|空闲线程保留最长时间|
|timeUnit|java.util.concurrent.TimeUnit|时间单位|
|workQueue|java.util.concurrent.BlockingQueue|指定使用哪一种BlockingQueue|
|threadFactory|java.util.concurrent.ThreadFactory|指定线程池创建线程的工厂，默认工厂类为Executors.defaultThreadFactory|
|handler|java.util.concurrent.RejectedExecutionHandler|指定当任务超限后的处理方式，默认处理类为AbortPolicy|

### jdk提供的线程池

|pool|corePoolSize|maximumPoolSize|keepAliveTime|timeUnit|workQueue|threadFactory|handler|
|-|-|-|-|-|-|-|-|
|newFixedThreadPool|参数指定|参数指定|0|TimeUnit.MILLISECONDS|LinkedBlockingQueue|Executors.defaultThreadFactory/参数指定|AbortPolicy|
|newSingleThreadExecutor|1|1|0|TimeUnit.MILLISECONDS|LinkedBlockingQueue|Executors.defaultThreadFactory/参数指定|AbortPolicy|
|newCachedThreadPool|0|Integer.MAX_VALUE|60|TimeUnit.SECONDS|SynchronousQueue|Executors.defaultThreadFactory/参数指定|AbortPolicy|
|newScheduledThreadPool|参数指定|Integer.MAX_VALUE|0|NANOSECONDS|DelayedWorkQueue|Executors.defaultThreadFactory/参数指定|AbortPolicy|

### execute
当调用executor.execute提交一个任务时，按照如下顺序处理： 
1. 如果当前线程数量少于核心线程数，则创建一个新的线程。
2. 如果当前线程数量大于等于核心线程数，但缓冲队列未满，则将新的任务添加到缓冲队列中，按照FIFO原则依次等待执行。
3. 如果当前线程数量大于等于核心线程数，且缓冲队列已满，但当前数量小于最大线程数，则创建新的线程。
4. 如果当前线程数量等于最大线程数，则调用handle方法处理。

## RejectedExecutionHandler

|类|处理方式|
|-|-|
|AbortPolicy|throw new RejectedExecutionException|
|CallerRunsPolicy|直接运行runable.run()|
|DiscardPolicy|丢弃|
|DiscardOldestPolicy|丢弃队列头部任务|

<p style="text-align: center"><strong>END</strong></p>