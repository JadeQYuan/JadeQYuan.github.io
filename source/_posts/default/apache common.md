title: apache common
categories:
  - default
description: apache common
author: Jade
date: 2020-04-05 09:28:00
---

一、Commons BeanUtils 
说明：针对Bean的一个工具集。由于Bean往往是有一堆get和set组成，所以BeanUtils也是在此基础上进行一些包装。 

二、Commons CLI 
说明：这是一个处理命令的工具。比如main方法输入的string[]需要解析。你可以预先定义好参数的规则，然后就可以调用CLI来解析。 

三、Commons Codec 
说明：这个工具是用来编码和解码的，包括Base64，URL，Soundx等等。用这个工具的人应该很清楚这些，我就不多介绍了。 

四、Commons Collections 
说明：你可以把这个工具看成是java.util的扩展。 

五、Commons Configuration 
说明：这个工具是用来帮助处理配置文件的，支持很多种存储方式 

六、Commons DBCP 
说明：Database Connection pool, Tomcat就是用的这个，不用我多说了吧，要用的自己去网站上看说明。 

七、Commons DbUtils 
说明：我以前在写数据库程序的时候，往往把数据库操作单独做一个包。DbUtils就是这样一个工具，以后开发不用再重复这样的工作了。值得一体的是，这个工具并不是现在流行的OR-Mapping工具（比如Hibernate），只是简化数据库操作，比如 

八、Commons HttpClient 
说明：这个工具可以方便通过编程的方式去访问网站。 

九、Commons IO 
说明：可以看成是java.io的扩展，我觉得用起来非常方便。 

十、Commons JXPath 
说明：Xpath你知道吧，那么JXpath就是基于Java对象的Xpath，也就是用Xpath对Java对象进行查询。这个东西还是很有想像力的。 

十一、Commons Lang 
说明：这个工具包可以看成是对java.lang的扩展。提供了诸如StringUtils, StringEscapeUtils, RandomStringUtils, Tokenizer, WordUtils等工具类。 

十二、Commons Logging 
说明：你知道Log4j吗？ 

十三、Commons Math 
说明：看名字你就应该知道这个包是用来干嘛的了吧。这个包提供的功能有些和Commons Lang重复了，但是这个包更专注于做数学工具，功能更强大。 

十四、Commons Net 
说明：这个包还是很实用的，封装了很多网络协议。 
1. FTP 
2. NNTP 
3. SMTP 
4. POP3 
5. Telnet 
6. TFTP 
7. Finger 
8. Whois 
9. rexec/rcmd/rlogin 
10. Time (rdate) and Daytime 
11. Echo 
12. Discard 
13. NTP/SNTP 

十五、Commons Validator 
说明：用来帮助进行验证的工具。比如验证Email字符串，日期字符串等是否合法。 

十六、Commons Virtual File System 
说明：提供对各种资源的访问接口。支持的资源类型包括 

1. CIFS 
2. FTP 
3. Local Files 
4. HTTP and HTTPS 
5. SFTP 
6. Temporary Files 
7. WebDAV 
8. Zip, Jar and Tar (uncompressed, tgz or tbz2) 
9. gzip and bzip2 
10. res 
11. ram 
这个包的功能很强大，极大的简化了程序对资源的访问。 


十七、Commons Transaction 
说明：提供持久层事务支持 

十六、Commons Proxy 
说明： 动态代理，拦截器一类的东西 

十八、Commons pool 
说明： 创建新的对象并初始化的操作，可能会消耗很多的时间。 
在需要频繁创建并使用这些对象的场景中，为了提供系统性能，通常的做法是，创建一个对象池，将一定数量的对象缓存到这个对象池中。 
需要使用时直接从对象池中取出对象，使用完后将对象扔回到对象池中即可。 
Apache的commons pool组件是我们实现对象池化技术的良好助手。 

十九、Commons Launcher 
说明：创建跨平台可执行程序 

二十、Commons Bean Scripting Framework（BSF） 
说明：是一个支持在Java应用程序内调用脚本语言 (Script)，并且支持脚本语言直接访问Java对象和方法的一个开源项目。有了它 , 你就能在java application中使用javascript, Python, XSLT, Perl, tcl, ……等一大堆scripting language 
. 反过来也可以，就是在这些scripting language中调用任何已经注册过了的JavaBean,java object。它提供了完整的API实现通过Java访问脚本语言的引擎。 

二十一、Commons chain 
说明： 可以在你需要定义和执行一些顺序操作的时候采用Commons Chain。 

二十二、Commons Compress 
说明： 是一个压缩、解压缩文件的类库。可以操作ar, cpio, Unix dump, tar, zip, gzip, XZ, Pack200 and bzip2格式的文件，功能比较强大 


二十三、Commons Discovery 
说明： 组件被用以查找可插拔接口的实现实例，它提供了一种通用的实例化这些实现的方式，而且可以管理单例（工厂）的生命周期。 

二十四、 commons exec 
说明： Apache Commons Exec 是 Apache 上的一个 Java 项目，提供一些常用的方法用来执行外部进程，如下面代码所示： 

String line = &quot;AcroRd32.exe /p /h &quot; + file.getAbsolutePath(); 
CommandLine commandLine = CommandLine.parse(line); 
DefaultExecutor executor = new DefaultExecutor(); 
executor.setExitValue(1); 
ExecuteWatchdog watchdog = new ExecuteWatchdog(60000); 
executor.setWatchdog(watchdog); 
int exitValue = executor.execute(commandLine); 

二十五、commons jelly 
说明：Jelly能够把XML转换成可执行代码,所以Jelly是一个基于XML与Java的脚本和处 理引擎。 Jelly借鉴了JSP定指标签，Velocity, Cocoon和Xdoclet中的脚本引擎的许多优点。Jelly可以用在命令行，Ant或者Servlet之中 

二十六、Commons FileUpload 
上传下载组件 
