title: Mybatis 源码
categories:
  - Java
  - 源码
description: Mybatis 源码
author: Jade
date: 2021-06-24 17:15:00
---

## Mybatis
MyBatis 是一款优秀的持久层框架，它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

## 关键类
- SqlSession
- Configuration
- TypeHandler
- Mapper
- Interceptor

## 流程
1. 获取SqlSessionFactory。
2. 解析xml配置文件。
3. 通过SqlSessionFactory创建SqlSession。
4. 通过SqlSession获取Mapper。
5. 通过Mapper调用方法。
6. Mapper为动态代理类，调用InvocationHandler的invoke方法。
7. 通过mapper调用的方法，及mapper的类名，获取MappedStatement，生成MapperMethod。
8. 通过MapperMethod，调用sqlSession的方法进行操作。
9. sqlSession的操作通过Executor实现。通过CachingExecutor或BaseExecutor中的doXXX执行。
10. doXXX方法通过Configuration创建StatementHandler，关联ParameterHandler及ResultSetHandler。
11. 插件处理，返回结果。

### 1.获取SqlSessionFactory

### 9.SqlSession、Executor
通过SqlSession调用的方法又调用Executor执行，那SqlSession的作用？ 1. 对外暴露多个重载方法，而对应同一个Executor方法；2. 对Executor方法抛出的异常进行处理。


	动态代理 - 接口、类加载器
	ognl表达式
	mapper 实例化、单例 
	Log
	TypeDiscriminator
	@Select <script> 与不加
	
1. 属性替换： 每次加载节点，转换为XNode数据时，在XNode构造方法中实现 ${} 属性替换。 即 XNode.evalNode("")时。
2. setting赋值顺寻：
3. TypeHandler中存储数据：保存在typeHandlerMap中。保存的是实例。如果javaType为null（实现TypeHandler接口 && 不适用注解  或者手动注册null），则忽略。
4. TypeHandler配置优先级： xml配置 > 注解 > 泛型（继承BaseHandler），手动使用TypeReference也会检查注解。
5. cache、cache-ref 只能存在一个且只能配置一份。 ？？？
6. 如果指定了databaseId，则每个sql、statement标签都需要指定databaseId。 ？？？
7. SelectKey
8. mapUnderscoreToCamelCase 默认false, 要真正存在一个与它对应的驼峰Bean才生效

### Configuration
- org.apache.ibatis.session
- typeHandlerRegistry
- typeAliasRegistry
- interceptorChain
- mapperRegister
- ScriptMap sqlFragments  解析sql标签的语句
- loadedResources  
	key： 	通过mapper标签指定url： url
			通过mapper标签指定resource： resource
			通过mapper解析namespace: `namespace:` + namespace
			通过java类解析：`interface ` + className
			通过java类解析相同名称及路径的xml：`namespace:` + className

- addMapper() / addMappers() -> mapperRegister.addMapper()/addMappers()

### BaseBuilder
- org.apache.ibatis.builder
- Configuration
- typeAliasRegistry
- typeHandlerRegistry

### XMLConfigBuilder extends BaseBuilder
- org.apache.ibatis.builder.xml
- XPathParser
- environment
- parse()

### XPathParser
- org.apache.ibatis.parsing
- Properties variables


### ResolverUtil<T>
- org.apache.ibatis.io
- 定义接口及实现类，进行条件匹配。
- 定义classloader、matches
- 根据接口查询、根据注解查询、根据条件查询

- 解析类有多步操作，用一个属性存储之前的结果，所有操作结束后调用方法返回所有结果。
- 接口参数后期才能确定，直接把接口作为参数。

### TypeAliasRegistry
- org.apache.ibatis.type
- 注册别名，不是匿名类、不是接口、不是成员类
- 获取注解指定别名
- 别名转小写
- 解析别名，不存在根据字符串解析，但不存储。
- 对基础类型及常用类型的保存。
- 直接根据类注册，跳过的类类型的判断。
- 根据别名、字符串注册与其它方式注册 加载类方式不一样，一种是直接通过classloader 加载，另一种通过resource加载。

### TypeHandlerRegistry
- org.apache.ibatis.type
- register  Map<Type, Map<JdbcType, TypeHandler<?>>> typeHandlerMap、 Map<Class<?>, TypeHandler<?>> allTypeHandlersMap：
	第一步：
		1. 查找MappedTypes注解，注册其每一个value。
		2. 判断是否实现TypeReference，若是，注册。
		3. 注册javaType为null。
	第二步： 
		1. 查找MappedJdbcTypes注册，注册其每一个value，并判断是否也需要注册jdbcType为null。
		2. 注册jdbcType为null。
	第三步：
		1. 若javaType不为null，则添加到typeHandlerMap。
		2. 以typeHandler.getClass()为key，添加到allTypeHandlersMap。
	添加方法：
		register(TypeHandler);
		register(Class, TypeHandler);
		private register(Type, TypeHandler);  相当于第一个通用处理方法。
		register(TypeReference, TypeHandler);
		register(Class, JdbcType, TypeHandler);
		private register(Type, JdbcType, TypeHandler); 第二个通用处理方法。
		另外支持TypeHandler 以Class为参数，通过getInstance转换， jdbcType不支持String。
		支持String代替Class，通过Resource转换。
		支持包名全部注册。
- register Map<JdbcType, TypeHandler<?>>  jdbcTypeHandlerMap： register(JdbcType, TypeHandler)。
- TypeHandler<Object> unknownTypeHandler
- Class<? extends TypeHandler> defaultEnumTypeHandler
- getTypeHandler:
	

### MapperRegistry
- org.apache.ibatis.binding
- Configuration
- Map<Class<?>, MapperProxyFactory<?>> knownMappers
- addMapper(Class) 最终执行方法
- addMappers(String packageName)
- addMappers(String packageName, Class superType)

### MapperProxyFactory
- org.apache.ibatis.binding
- Class mapperInterface
- Map<Method, MapperMethodInvoker> methodCache


### XMLMapperBuilder extends BaseBuilder
- org.apache.ibatis.builder.xml
- parser
- MapperBuilderAssistant mapperBuilderAssistant
- sqlFragments
- parse()


### MapperAnnotationBuilder
- org.apache.ibatis.builder.annotation
- configuration
- mapperBuilderAssistant
- type
- 解析：
	解析Cache: @CacheNamespace
	解析CacheRef: @CacheNamespaceRef
	解析ResultMap: 


### MapperBuilderAssistant extends BaseBuilder
- org.apache.ibatis.builder.xml
- namespace
- resource

### XMLStatementBuilder extends BaseBuilder
- org.apache.ibatis.builder.xml
- mapperBuilderAssistant 为XMLMapperBuilder的成员变量


### Q&A
1. mapper通过url、resource、class加载，且xml会加载class，class会加载xml，怎么去重
	所有的资源都在configuration的loadedResources中保存，加载xml其key为resource路径/url路径，加载class其key为 class.toString(), 通过class加载xml与通过xml加载class 都是通过全限定类名/namespace查询加载，其key相同，为 `namespace:` + 全限定类名。
2. 加载class -> 先加载xml -> xml加载完查询class加载 —> ... 会一直加载下去么
	class的加载，都需经过mapperRegistry的addMapper()方法， 先行存储加载的class。
	通过xml加载后，会根据namespace加载class，并在此判断mapperRegistry中是否已加载该class。
3. 会不会加载完xml找不到对应的class，从而getMapper拿不到实体
	xml可以加载，mapper拿不到。
4. getMapper()返回的代理类是每次创建么，如果不是，怎么保存的
	不是，因为每次调用的sqlSession是不同的，创建出来的代理的sqlSession为当前sqlSession。
5. mybatis获取不到接口的参数名，而只能使用param1、param2之类的
	java在编译的时候，默认不会保留方法名参数，因此无法在运行时获取参数名称。
	编译时可以使用-g参数来保留方法名参数。
	maven在编译时会默认添加-g参数，所以通过maven可以拿到具体方法名参数。
6. resultMap标签中的type、ofType、javaType、resultType
	type: resultMap标签的属性，为类的全限定名称，表示返回的结果。
	ofType：collection标签的属性，表示哪一种类型的集合。
	javaType：property标签的属性，表示这个属性的类型。
	resultType：select标签的属性。
7. XmlMapperBuilder、MapperBuilderAssistant、MapperAnnotationBuilder
	XMLMapperBuilder、MapperAnnotationBuilder 继承自BaseBuilder，为什么AnnotationMapperBuilder没有呢？
	XMlMapperBuilder、MapperAnnotationBuilder都定义了MapperBuilderAssistant属性，是抽象公用？
	因为除了AnnotationMapperBuilder，其它都是解析xml，BaseBuilder提供了将字符串解析为对象的方法，而注解可以直接使用类型定义。
	MapperBuilderAssistant相当于工具类，且需要使用BaseBuilder的基础方法。
8. 为什么XML和DAO中的ResultMap不能通用呢？
	注解方式ResultMap是通过 类名、方法名、方法参数 拼起来的， 可以通过@Results的id属性指定。
	XML方式是显示id和namespace拼接的，xml的id必须指定，通过dtd约束。
	使用解析后的resultMapId是可以通用的。
9. MapperProxy中的MapperMethodInvoker与使用函数式接口的区别。
	1. 通过接口能体现出多态的特性。
	2. 接口需要在其它地方引用。


### 
1. MapperRegistry中config属性只为创建XmlAnnotationBuilder，没有其它使用地方。将其作为全局变量来存储，而不是方法参数带过来。

## SqlSessionFactory

#### 构建方式
1. 通过xml方式
   将配置信息放在xml中，然后通过加载xml配置文件，使用SqlSessionFactoryBuilder来创建。
2. 通过java代码
   通过DataSource、 Environment、 TransactionFactory、 Configuration 等类来创建。
3. 通过spring
   // TODO
   3.1 通过xml
   3.2 通过yml

## SqlSession

#### 构建
	try (SqlSession session = sqlSessionFactory.openSession()) {
		...
	}

## 映射

#### 映射器
	绑定映射语句的接口。

## configuration
- properties
- settings
- typeAliases
	1. 通过typeAlia标签配置
	2. 通过package标签及@Alias注解（没有注解时使用Java Bean首字母小写的非限定类名）配置
- typeHandlers
	1. 通过typeHandler标签配置
	2. 通过package标签
- objectFactory 无自动义的情况下使用默认的DefaultObjectFactory.java
- plugins
  Executor (update, query, flushStatements, commit, rollback, getTransaction, close, isClosed)
  ParameterHandler (getParameterObject, setParameters)
  ResultSetHandler (handleResultSets, handleOutputParameters)
  StatementHandler (prepare, parameterize, batch, update, query)
- environments
  每个environment 包含transactionManager 和 dataSource 配置‘
  transactionManager 配置事务的提交和回滚规则，使用数据库提供的（type=JDBC），还是自己配置的（type=MANAGED）。
- databaseIdProvider
- mappers
	1. 通过mapper标签，使用resource/URL/class属性。
	2. 通过package标签


## 设计模式
- 工厂方法： SqlSessionFactory。
- 代理： CachingExecutor（代理控制对象的访问，装饰器增加对象的行为）。RoutingStatementHandler（这里应该可以使用简单工厂）。
- 责任链： Interceptor。
- 模板方法： BaseExecutor。
