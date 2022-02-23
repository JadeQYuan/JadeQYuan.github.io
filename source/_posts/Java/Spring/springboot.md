title: spring
categories:
  - Java
  - Spring
description: spring
author: Jade
date: 2020-07-14 18:13:00
---

## spring-boot-maven-plugin

java并没有提供加载嵌套jar文件的标准方式。 通过该插件，将程序打包为一个可执行的jar文件，该文件可在生产环境中运行。 如果不添加该插件，则打包后无法执行，只能供其它项目引用。

## spring-boot-starter-parent

作为springboot的父级项目，提供以下功能：

- 使用JDK1.8做为默认的编译器级别。
- UTF-8源码编码。
- dependencyManagement，管理公共依赖的版本。
- 资源过滤。
- 插件配置。

PS:

- 可以通过在项目中设置属性来覆盖各个依赖项。 ex: 修改spring-data的版本

```xml
<properties>   
    <spring-data-releasetrain.version>Fowler-SR2</spring-data-releasetrain.version>
</ properties>
```

- 由于properties和yml文件接受spring样式占位符“${...}”，Maven过滤器被更改为使用"@...@"作为占位符，可通过配置resource.delimiter自定义。
- 可以不使用默认parent配置，自定义父级依赖。但仍然可以使用scope=import的方式来引入依赖。

## starter

是一套方便的依赖描述符，可以获取spring及相关技术的一站式商店，无需查看代码示例并复制粘贴依赖描述符。

## @EnableAutoConfiguration

- 通常建议将主类放在其他类上方的根包中，并使用@EnableAutoConfiguration注解该类。  
- 当主类在其他类上方的根包中时，使用@ComponentScan可以不指定basePackage。

## spring-boot-devtools

- 默认禁用缓存，某些库可使用缓存来提供性能，例如 thymeleaf。  
- 通过类加载器来实现自动重启，只丢弃有修改的类并创建一个新类，提高启动速度。  
- devtools监控资源类路径，触发重启的唯一方法时更新类路径，更新方式取决于IDE。  
- 默认情况下，静态资源和模板改变不回触发自动重启。  
- 可以使用触发文件，可定时/手动更新触发文件以自动重启。

## 监听器

1. 所有的监听器都需继承ApplicationListener<ApplicationEvent>。
2. 所有的事件都需继承ApplicationEvent。
3. 可以自定义事件，自定义监听器，监听器只会监听配置的事件及其子类。

## 拦截器

1. 定义。实现HandleInterceptor接口，根据情况实现其对应的方法。
2. 注册。继承WebMvcConfigurationSupport 或 实现WebMvcConfigurer接口，重写addInterceptors方法。  
   PS: 使用拦截器拦截全部请求路径会导致静态资源也不能访问，可以根据情况进行配置。

## 过滤器

1. 使用@WebFilfer注解配置。
2. 实现Filter接口。

## CommandLineRunner & ApplicationRunner

在SpringApplication.run(...)完成之前调用。

## Profiles
- 编程方式  
- 配置文件

## 日志
