title: classloader
categories:
  - Java
tags: []
description: classloader
author: Jade
date: 2021-09-03 15:08:00
---
1. classloader
	将class文件加载到jvm虚拟机中，使得程序可以运行。
	jvm启动时，并不会一次性加载所有class文件，而是根据需要动态加载。 ？？？

2. 系统类加载器
	1. Bootstrap ClassLoader  加载环境变量[sun.boot.class.path]目录下jar和class。
	2. Extention ClassLoader  加载环境变量[java.ext.dirs]目录下jar和class。
	3. AppClass Loader 加载环境变量[java.class.path]目录下jar和class（项目当前路径）。
	4. 如需加载其它路径，或重写加载规则，需自定义classLoader。
	5. 每个classLoader都有一个parent，在创建时指定。AppClassLoader的parent为ExtClassLoader，自定义parent默认为AppClassLoader。
	6. Context ClassLoader - Thread ClassLoader，线程默认加载器为AppClassLoader，可自行设置更改，子线程会继承父线程的ClassLoader。
	

3. 双亲委派机制
	如果一个类加载器收到类加载的请求，它首先不会自己去尝试加载这个类，而是把这个请求委派给父类加载器完成。每个类加载器都是如此，只有当父加载器在自己的搜索范围内找不到指定的类时，子加载器才会尝试自己去加载。
	
	优点：
		安全、性能（避免重复加载，避免核心类被篡改）。
	
	缺陷：
		基础类无法调用用户类。
		（不知道具体实现类，无法创建对象）
		（如果类A中调用了类B，那么加载B的时候，需要使用A的类加载器去加载B。
		如果A是基础类，B是用户类，那么A对应的最上层类加载器，是没办法处理下层的用户类的。）
		
	解决：
		SPI + Thread ClassLoader。
		1. SPI只是一种机制/规范，具体加载部分还是使用Thread ClassLoader加载。
		2. 使用Thread ClassLoader 破坏了双亲委派机制。

4. 加载
	1. 虚拟机启动时，加载执行的主类。
	2. new、getstatic、putstatic、invokestatic字节码指定。
		1. 使用new实例化对象。
		2. 读取/设置静态字段。
		3. 调用静态方法。
	3. 使用反射调用。
	4. 加载子类时，父类未被加载，优先加载父类。
	
	不会加载
		1. 常量在编译阶段会存入调用类的常量池中，使用常量不会加载。
		2. 创建数组不会加载。
		3. 通过子类引用父类静态属性/方法，只会加载父类。

5. Launcher
	Launcher是jvm的启动类。
	
	