title: AOP
categories:
  - Java
description: AOP
author: Jade
date: 2020-02-05 11:04:00
---

## 一. 什么是AOP
	AOP（Aspect Oriented Programing），面向切面编程，是对OOP的补充，通过预编译方式或运行期动态代理实现程序功能的统一维护的一种技术。
## 二. 意图
	将与业务无关的代码，如日志记录，性能监控，事务处理等从业务逻辑代码中划分出来，将它们独立到非业务逻辑方法中，使得与业务方法解耦，并且在改变相关逻辑的时候不影响业务逻辑的代码。
## 三. AOP 概念
#### 切面 Aspect
	切面是一个横切关注点。
#### 连接点 JointPoint
	连接点是具体执行增强的点，比如方法执行，构造器调用，成员赋值。
#### 切点 PointCut
	匹配连接点的正则表达式，是连接点的集合。
#### 通知 Advice
	对连接点的进行的操作。
#### 织入 Weaving
	把切面应用到目标对象，并创建代理对象的过程。切面在指定的连接点被织入到目标对象。
## 四. AOP流行框架比较
	当下最流行的AOP框架为Spring AOP 及 AspectJ。
1. 能力和目标
- Spring AOP
	旨在通过Spring IOC 提供一个简单的AOP实现。
	不是一个完整的AOP解决方案，只能用于被Spring容器管理的bean。
- AspectJ
	完整的AOP解决方案，比Spirng AOP复杂。
	可以在应用于所有领域对象。
2. 织入时机
- Spring AOP
	只能在运行时织入。
- AspectJ
	可以在编译期，加载期，编译后（jar包和字节码文件）。
3. 依赖
- Spring AOP
	使用JDK动态代理或者VGLIB代理。
- AspectJ
	不依赖任何运行时环境，只需要AspectJ compiler(ajc)在运行前完成织入。
4. 连接点
- Spring AOP
	由于要使用代理模式，所以不能作用域final类，static方法，final方法。
	只支持方法执行连接点。
- AspectJ
	没有限制。
	方法调用，方法执行，构造器调用，构造器执行，静态初始化执行，对象初始化，成员引用，成员赋值，处理器执行，通知执行。
5. 复杂度
- Spring AOP
	不需要额外的编译器，只能和Spirng管理的bean一起工作。
- AspectJ
	需要引入ajc并重新打包。
6. 总结

|Spring AOP|AspectJ|
|-|-|
|Implemented in pure Java|Implemented using extensions of Java programming language|
|No need for separate compilation process|Needs AspectJ compiler (ajc) unless LTW is set up|
|Only runtime weaving is available|Runtime weaving is not available. Supports compile-time, post-compile, and load-time Weaving|
|Less Powerful – only supports method level weaving|More Powerful – can weave fields, methods, constructors, static initializers, final class/methods, etc…|
|Can only be implemented on beans managed by Spring container|Can be implemented on all domain objects|
|Supports only method execution pointcuts|Support all pointcuts|
|Proxies are created of targeted objects, and aspects are applied on these proxies|Aspects are weaved directly into code before application is executed (before runtime)|
|Much slower than AspectJ|Better Performance|
|Easy to learn and apply|Comparatively more complicated than Spring AOP|

### 参考
	https://www.baeldung.com/spring-aop-vs-aspectj

