1. eureka server
依赖
	spring-cloud-starter-eureka-server
注解
	@EnableEurekaServer

配置
	spirng.application.name server需要么
	eureka.clinet.service-url.default-zone ？？？
	eureka.clinet.registry-with-eureka 如果有集群，是否注册到其他eureka服务
	eureka.client.fetch-registry
	
自我保护模式
数据中心
环境

2. eureka clent
依赖
	spring-cloud-starter-eureka
注解
	@EnableEurekaClinet  只能被eureka服务中心发现
	@EnalbeDisconveryClient  可以被其他服务注册中心发现

配置
	spring.application.name 指定服务名称
	eureka.client.service-url.default-zone
	eureka.clent.instance.perfer-ip-address
	eureka.client.instance-id  指定服务实例id,默认为 主机名:服务名:端口
	

3. ribbon 编程式服务间调用、负载均衡
依赖
	spring-cloud-starter-ribbon

注解
	@LoadBalanced
	@RibbonClient

4. feign 声明式服务间调用
注解
	@EnableFeignClients
	@FeignClient

配置
	spring.

feign对hystrix的支持
feign中callback及callbackfactory的属性设置

5. hystrix 熔断处理
@HystrixCommand

6. 网关
注解
	@EnableEuulProxy  组合注解

配置
	zuul.routes.***.path
	zuul.routes.***.service-id/url

7. config



8. sleuth 全链路追踪

9. log 
ESK  ES、LogStash、Kibana


turbine
	
	
	
通过在不同环境中配置 port，来启动多个spingboot实例  @Import
spring mvc Resolver
启动异步 @EnableAsync 方法使用@Async(调用方与执行方在两个service里)
@Transaction rollbackfor 默认为受检异常
starter核心 auto-configuration
session、Token、JWT
@Mappper
springboot parent、dependencies