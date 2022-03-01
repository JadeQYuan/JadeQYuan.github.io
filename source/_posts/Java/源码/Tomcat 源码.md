title: Tomcat 源码
categories:
  - Java
  - 源码
description: Tomcat 源码
author: Jade
date: 2022-01-27 13:00:00
---
  
## Tomcat
- Tomcat具有接受并处理Http请求的能力，所以Tomcat是Http服务器。
- Tomcat满足Servlet接口和协议，所以Tomcat是Servlet容器。
- Web服务器对应Coyote框架，具体为Connector组件。
- Servlet容器对应Catalina容器，具体为Container组件。
- Tomcat主要运行JSP和Servlet，处理静态HTML的能力不如Apache服务器。

## 术语
- Catalina，Tomcat内部Servlet容器。
- Coyote，Tomcat连接框架。
- JMX，Java Management Extensions。

## 关键类
- Bootstrap，Catalina启动加载类。
- Catalina，为Catalina容器处理shell命令。
- Server(StandardServer)，代表整个Servlet容器，NamingResources最顶层，包含一个或多个Service。
- Service(StandardService)，包含一个或多个Connector，共享一个Container，Container处理从Connector来的请求。
- Connector，Coyote Connector的实现。
- Container，处理请求并相应的对象。实现类按层级为Engine（Servlet引擎）、Host、Context、Wrapper。
- Lifecycle，Catalina组件生命周期接口。
- PipeLine、Valve，控制和/或修改请求和响应。
  
## 流程
1. startup.bat -> catalina.bat -> Bootstrap。
2. bat中引用的变量，设置的参数，执行的命令等。
3. Bootstrap类静态加载使用System.getProperty获取数据，而这是启动类，所以应该是命令行参数传递过来的。
4. Bootstrap使用反射调用Catalina方法原因分析。
5. 解压tomcat\bin\bootstrap.jar。
6. Bootstrap初始化类加载器，最后通过AccessController.doPrivileged。
7. 初始化了三个类加载。都是URLClassLoader的实例，顺便看一下JVM源码里面的类加载器结构。这块还有Thread.contextClassLoader。
8. Bootstrap反射调用了Catalina的load、start方法，但是server为null，且无设置地方。分析load方法中的解析server.xml部分。
9. 根据XML中的配置及一些默认配置，对组件进行处理。且每个组件负责其子组件的处理。处理主要包括initial、start。另外还有监听器。
10. Container组件监听器。
11. ContextConfig解析context.xml、web.xml。
12. Pipeline与Valve。

### 1.tomcat启动流程
   tomcat/bin/startup.bat -> tomcat/bin/catalina.bat -> org.apache.catalina.startup.Bootstrap。
   在eclipse中，使用javaw指令。

### 2.CATALINA_HOME、CATALINA_BASE、JAVA_HOME、jdb、jpda、juli
   CATALINA_HOME环境变量，应该设置tomcat根目录，而不是tomcat\bin目录。如果没有设置，tomcat只能在tomcat目录和bin目录下执行，其它目录下执行找不到对应的catalina.bat文件。
   catalina.bat中引用了JAVA_HOME的环境变量。

### 3.java -Dproperty=value
   -D set a system property value。
   tomcat可以设置 catalina.home、catalina.base 两个参数。
   在Bootstrap中，使用了System.getProperty，set操作是在命令行进行的。
   在catalina.bat中，对catalina.home、catalina.base做了判断赋值。

### 4.Bootstrap使用反射调用Catalina方法，包括new、load、start。
   通过反射进行解耦。
   启动时添加了classpath为tomcat\bin\bootstrap.jar，其中没有Catalina类。通过配置文件，使用ClassLoader加载tomcat\lib\下面的jar。（Bootstrap.initClassLoaders）
    1. commonClassLoader做为catalinaClassLoader和shareClassLoader的parent。
    2. CatalinaProperties使用静态初始化加载配置文件。
    3. 配置文件顺序： 1.命令行指定-Dcatalina.config； 2.tomcat目录tomcat\conf\catalina.properties文件； 3.bootstrap.jar中org.apache.catalina.startup.catalina.properties文件。

### 5.bootstrap.jar中只使用了几个类
   Bootstrap 主类
   CatalinaProperties 加载配置文件
   ClassLoaderFactory 创建类加载器，并指定相应的parent
   Constants 常量
   SafeForkJoinWorkerThreadFactory
   Tool

### 6.AccessController.doPrivileged
   Java安全： 沙箱 -> 代码签名 -> 权限 -> 域（系统域、应用域）
   使用-Djava.security.SecurityManage开启权限验证。指定policy文件。不指定使用JDK默认的。
   AccessController.checkPermission 验证权限，会验证操作栈中每一个栈帧的权限。
   AccessController.doPrivileged 验证权限，只在当前栈帧验证，中断栈上验证的操作。
   acc AccessControlContext。
   tomcat\conf\catalina.policy。

### 7.URLClassLoader
   JDK11
   null(ClassLoaders.BootClassLoader) -> platform(ClassLoaders.PlatformClassLoader) -> app(ClassLoaders.AppClassLoader)
   JDK8
   null(BootstrapClassLoader) -> Launch.ExtClassLoader -> Launch.AppClassLoader
   CLassLoader: app -> commonLoader -> catalinaLoader、sharedLoader   catalina.parentClassLoader = shared。

### 8.server.xml 解析
   org.apache.tomcat.util.digeter包。
   Digester[Rules, ArrayStack, SAXPaser、XMLReader]。
   digester.parse -> getXMLReader(设置handler，DTDHandler、ContentHandler、EntityResolver、ErrorHandler) -> xmlReader.parse -> 解析xml，调用各种handler处理 -> 根据标签信息，获取对应的rule -> 调用rule创建对象、设置属性、调用方法等。

### 9.Lifecycle
状态：New、Initializing、Initialized、Starting_Prep、Starting、Started、Stop_Prep、Stopping、Stopped、Destroying、Destroyed、Failed。
事件：before_init、after_init、start、before_start、after_start、stop、before_stop、after_stop、before_destroy、after_destroy、periodic、configure_start、configure_stop。
StandardServer初始化：StandardService初始化。
StandardService初始化：Connector初始化，Container初始化。
...

### 10.Container组件监听器
EngineConfig:
HostConfig:
ContextConfig:

### 11.解析context.xml、web.xml
context.xml: config/context.xml +> EngineName/HostName/context.xml.default +> META-INF/context.xml。
web.xml: config/web.xml +> EngineName/HostName/web.xml.default +> WEB-INF/web.xml +> WEB-INF/lib/!jar/META-INF/web-fragment.xml。

### 12. Pipeline与Valve
对request处理 -> 调用getNext().invoke() -> 对response处理。
如果valve不通过，则不调用getNext().invoke()。
pipeline中只保存了第一个valve，而valve之间使用责任链的方式进行处理。
每个Container中都有一个basicValve，用来处理下级容器的valve，直到WrapperValve处理Servlet。

## 设计模式
- 模板方法：LifecycleBase。
- 简单工厂：ApplicationFilterChain。
- 责任链：Valve、FilterChain。
- 观察者：Lifecycle、LifecycleEvent、LifecycleListener。

## TODO
- 加载web.xml，loadOnStartUp。
- 封装Servlet，Request、Response。
- tomcat配置，context标签。
- 生命周期接口。
- Web容器、Servlet容器实现区分。
- tomcat架构图/server.xml配置文件的理解。
- NIO的使用。

## Q
- org.apache.catalina  org.apache.tomcat
- tomcat maven插件与tomcat-embeded版本有什么区别
- tomcat maven插件配置完启动的tomcat是在哪里
    1. 添加tomcat maven插件后在依赖里并没有相关的包。
    2. 将依赖下载的jar包解压，找到pom文件，里面依赖的是tomcat-embeded等。jar包比spring-boot-starter-tomcat中依赖的tomcat jar包要多。
    3. 解压包里面有一些配置文件，使用的还是tomcat本身的配置文件，而tomcat-embeded里面没有找到。
