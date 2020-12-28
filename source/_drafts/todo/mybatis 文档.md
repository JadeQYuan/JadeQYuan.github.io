## SqlSessionFactory

#### 构建方式
1. 通过xml方式
	将配置信息放在xml中，然后通过加载xml配置文件，使用SqlSessionFactoryBuilder来创建。
2. 通过java代码
	通过DataSource、 Enverionment、 TransactionFactory、 Configuration 等类来创建。
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
	每个environment 包含transactionMangager 和 dataSource 配置‘
	transactionManager 配置事务的提交和回滚规则，使用数据库提供的（type=JDBC），还是自己配置的（type=MANAGED）。
 - databaseIdProvider 
 - mappers 
	1. 通过mapper标签，使用resource/URL/class属性。
	2. 通过package标签