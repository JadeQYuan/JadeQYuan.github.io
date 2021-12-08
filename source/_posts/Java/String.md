title: String
description: String
categories:
  - Java
author: Jade
date: 2021-11-15 15:48:00
---

在C/C++中，字符串作为字符的数组被实现。而在Java中，字符串是作为对象实现，字符串实际上是对象类型。

Java字面量：
	基本数据类型
	字符串
	数组 - 实际也是对象？

字符串常量池： 在类加载时，在堆（方法区？）中创建一个对象，然后将它的引用存放在池中（还是方法区？）的一个常量表中。并且不会被垃圾回收。

使用new创建字符串，是在运行期创建的。

String s1 = "abc";
String s2 = new String("abc");
s1.equals(s2) && s1 != s2 && s1.value == s2.value
字符串的值使用数组实现，在java中也是对象，s1，s2 的值都指向常量池中的数组对象。

String intern(): 把自身替换为常量池中的引用

字符串拼接：
	字面量拼接： 优化为一个字面量
	字面量和变量拼接： 使用StringBuilder优化
	int + char -> char
	int + string -> string
	string + 任意 -> string
	


String 实现方式
	Jdk 6 char[]、offset、count、hash
	Jdk 7、8  char[]、hash
	Jdk 9  byte[]、coder、hash  

	
数组：
	数据是对象，但不是从某个类实例化来的，而是由JVM直接创建的，其父类是Object。
	每个数据都对应一个Class对象，通过RTTI，可以检查数据的运行时类型，签名，基类等。
	
	数组		RTTI
	char[]		[C
	int[]		[I
	long[]		[J
	float[]		[F
	String[]	[Ljava.lang.String;

字面量初始化
int  		直接定义, int i = 1;
short 		2个字节以内的int，short s = (short)1;
long		l/L 结尾
byte		1个字节以内的byte，byte b = (byte)1;
float		f/F 结尾
double		整数+d/D结尾或小数
char		单引号
boolean 	true/false
string		双引号
[]			大括号{} （简化了new）

null		null

null：
	null是一种数据类型，但可以忽略。
    null是关键字，是所有对象类型的默认值。


