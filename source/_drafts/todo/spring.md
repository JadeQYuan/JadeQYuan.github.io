service实现多个接口，则用任一接口都可注入该对象

1. spring IOC 
	加载
		1. 加载配置文件、读取配置
		2. 扫描包
		3. 实例化、放入容器
		4. 自动注入
	初始化
		5. 请求映射
	
2. Spring MVC
	1. 加载配置文件、读取配置
	2. 扫描包
	3. 实例化、放入容器
	4. 自动注入
	5. 请求映射
	
	6. 请求分发、参数封装、校验等
	
入口
	ClassPathXmlApplicationContext
	AnnotationConfigApplicationContext
	
注入方式
	1. @Controller @Service @Repository @Commonent
	2. @Bean
	3. @Import
	4. FactoryBean

注解驱动
IOC
1. @Configuration
	配置类相当于配置文件
	@Bean相当于bean标签，返回值相当于bean标签class，方法名作为默认key，也可自定义
	@Configuration被@Component注解，本身相当于一个bean
2. @ComponentScan
	相当于<context:component-scan />标签
	includeFilters、excludeFilters 相当于标签属性  includeFilters 需要将userDefaultFilters置为false
	@ComponentScans 配置多个
	自定义TypeFilter
3.@Scope
	Prototype(多实例)、Singleton（单例）、Request、Session
	Singleton 容器启动会创建对象放入容器
	Prototype 每次获取时创建新的对象、不会管理
4. @Lazy
	针对单例bean，在第一次调用的时候创建并放入容器
	
5. @Conditional spring4.x新增
	按照一定的条件进行判断，满足条件创建bean并放入容器
	实现Condition接口
6. @Import
	value为class，容器中注入该类对象，key为class全限类名
	实现ImportSelector接口, 返回全限类名数组
	实现ImportBeanDefinitionRegistrar接口，实现自定义注册BeanDefinition
7. FactoryBean 接口
	默认获取到的是getObject返回的bean，加&前缀获取本身
8. 生命周期 自定义
	xml配置 bean标签属性：init-method destroy-method， @Bean属性 initMethod destroyMethod
	Bean 实现 InitalizBean、DisposingBean 接口
	使用@PostConstruct @PreDestroy 注解
	Bean实现BeanPostProcessor接口 spring 底层对BeanPostProcessor的使用
9. @Value
	字面量
	SPEL、 #{}
	${} 取配置文件的值  @PropertySource/@PropertySources 指定读取的配置文件， 相当于xml中的<context:property-placeholder />
10. 自动装配
	@Autowired 先按类型匹配，如果找到多个，按属性名为key匹配 required 属性指定是否必须
	@Primary 按类型匹配多个时，注入@Primary注解的bean，而不使用属性名，可使用@Qualifier注入其他bean
	@Qualifier 按类型匹配多个时，指定按照key去匹配
	@Resource JSR250 java规范 默认按属性名称注入，可自定义key，无法和@Pramiry、@Qualifier 组合使用，没有required属性
	@Inject JSR330 java规范 需要添加依赖 javax.inject, 和 @Autowired 规则一样，没有required属性

	@Autowired 
		标注在方法上，spring创建容器时会调用标注了该注解的方法  可以 @Bean + 方法参数，注解可省略
		标注在构造器上 一样  如果只有一个有参构造器，该注解可以省略
		标注在参数 一样
	Aware
		创建对象的时候，调用相应的方法，实现注入
		使用PostProcessor实现
	@Profile spring 提供的根据当前环境，动态激活和切换一系列组件的功能	
		激活 默认为"default" 
			虚拟机 -Dspring.profiles.active= 
			代码 applicationContext.getEnvironmet.setProfile() 需要容器创建前设置
			
AOP
切面、切点、通知
<aop:aspectj-autoproxy> @EnableAspectJAutoProxy
1. @Befor @After @AfterReturning @AfterThrowing @Around @PointCut @Aspect @EnableAspectJAutoProxy JointPoint必须是第一个参数
2. @EnableAspectJAutoProxy -> @Import -> ImportBeanDefinitionRegistrar
	
事务
@Transactional <tx:annotation-driver> @EnableTranscationManagement
配置事务管理器 PlatformTransactionManage DataSourceTransactionManager

事件
@EventListener EventListenerMethodPostPossector, 可在方法上使用
@Commonent  +  ApplicationListener 


Web Sevlet3.0+以上支持注解
Web三大组件 Servlet Filter Listener
@WebSevlet
@WebFilter
@WebListener
@WebInitParam
ServletContainerInitializer
异步请求	支持、开启、配置


MVC
@EnableWebMvc  <mvc:annotation-driver />
WebMvcConfigurer接口的方法相当于xml里面的mvc配置


过滤器、拦截器

refresh









