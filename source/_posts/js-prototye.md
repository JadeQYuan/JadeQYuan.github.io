title: js prototye
categories:
  - JS
tags: []
description: js prototye
author: Jade
date: 2021-07-29 16:08:00
---
1. __proto__ 和 contructor 是对象属性，prototype是函数属性（函数也是对象）。
2. __proto__ 由一个对象指向它的原型对象。
3. prototype 从一个函数指向所创建实例的原型对象。
4. contructor 从一个对象指向给对象的构造函数。


## prototype 的目的
共享方法、共享属性、面向对象

1. 函数内部定义的变量及函数，只能在内部调用，是私有的，外部无法访问。
2. 函数添加静态变量及函数，通过函数对象本身可以访问，但是通过实例访问不到。
3. 函数内部通过this添加变量及函数，创建实例时详单与做了拷贝，无法共享。（函数本身拷贝没有意义，且浪费资源）

故，只要创建一个函数，就为该函数创建一个prototype属性，prototype本身是个对象，其contructor属性指向该函数本身，其__proto__属性指向Function.prototype。

## 对象创建方式及区别

1. 字面量创建
	__proto__ 指向Object.prototype。
2. 函数对象
	__proto__ 指向Function.prototype。
	prototype 指向 该对象的prototype。
3. new创建
	1. 生成一个新对象
	2. 设置对象__proto__指向函数的prototype属性。
	3. 绑定this
	4. 返回
	
## 构造函数
	内部使用this变量，使用new调用创建。
	构造函数生成的实例对象都有__proto__属性，指向构造函数的prototype。
	利用构造函数继承属性，利用原型对象继承方法。（组合继承）

## class
	构造函数的另一种写法。
	语法糖。
	
## 继承
	1. 原型链继承
	2. 构造函数继承
	3. 组合继承
	其它。。。
