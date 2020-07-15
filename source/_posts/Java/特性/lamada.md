title: lamada
categories:
  - Java
  - JDK8
tags: []
description: lamada
author: Jade
date: 2020-02-05 11:04:00
---

lamada 本质上可以理解为匿名内部类，在编译时传入的是实现了方法接口的匿名内部类。

lamada VS 匿名内部类
1. 匿名内部类编译后会出现 类名$1.class 的字节码，lamada没有。
2. 通过反编译（javap），lamada在类中创建了一个 lamada$所在方法名$1 的static方法。
3. 匿名内部类通过构造函数传入了一个原类的final实例。

==？？？lamada是怎么访问方法局部变量的？？？==

## 函数式接口
#### java8 内置核心函数式接口
1. Consumer<T> 消费型
	void accept(T t);
2. Supplier<T> 提供型
	T get();
3. Function<T, R> 函数型
	R apply(T t);
4. Predicate<T> 断定型
	boolean test(T t);
#### java8 其它函数式接口

<p style="text-align: center"><strong>END</strong></p>
