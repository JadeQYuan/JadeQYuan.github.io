title: mybatis
categories:
  - Mybatis
description: mybatis
author: Jade
date: 2020-07-14 14:12:00
---

- mybatis 基于注解的sql可以不用写script？  
	script 标签中可以使用xml中的标签来实现复杂语句的查询
- mybatis 多个参数时使用@Param 注解指定？
	不使用@Param注解：
		参数为基本类型，可以有多个
		参数为javabean对象，且只能有一个，使用时直接用对象的属性（注解无法获取多个属性，只能获取嵌套属性）
	参数为String时，必须指定@Param注解，但是当有多个参数时，可以不用注解，猜想可能是把多个参数自动封装成一个对象了
- mybatis 基于注解使用@ResultMap("?") 来使用xml中定义的reslutmap
	只能引用通过@Result注解定义的，并指定名称的resultmap
- 当方法传入多个参数且包含复杂对象时，使用 对象.属性 来引用，可以使用@Param起别名。如果其中有基本参数类型，直接引用即可。

