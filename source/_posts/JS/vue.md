title: vue
categories:
  - JS
description: vue
author: Jade
date: 2021-07-29 16:08:00
---

- ES6在语言的层面上实现了模块化。浏览器厂商和 Node.js 都宣布要原生支持该规范。它将逐渐取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。


VUE项目打包后通过nginx代理找不到js/css文件
- nginx代理后路径为 root 路径 + location 路径
- 需要修改VUE static 打包路径为 location 路径 + static (相对路径)
- 需要修改VUE index.html 打包路径为 location 路径下的index.html  或者 修改 nginx 配置 try_files 为 location 路径/index.html

	__dirname ： js文件当前绝对路径（仅在js文件中有效）
	path： node 内置模块
	index: 打包后 index.html 文件路径 （绝对路径） 
	assetRoot: 指向包含应用程序的所有静态资源的根目录
	assetsSubDirectory: 静态资源要存放的路径， 相对于 assetRoot 的路径
	assetsPublicPath: 代表打包后，index.html里面引用资源的的地址 （相对路径/绝对路径）


eslint 文件/设置中 区别，关系
-文件：运行项目后，通过控制台才发现语法错误。
-设置：在开发过程中，就根据ESlint规则修改代码。（不必支持项目）
IDEA中配置：Setting ->Preferences -> Languages & Frameworks -> JavaScript -> Code Quality Tools -> Eslint ，然后勾选Enable单选框。


		IDEA webpack配置
	- 当在“设置/首选项”|语言和框架|JavaScript|Webpack中打开项目或编辑指定的webpack.config.js时，IntelliJ IDEA在后台分析配置，并根据收到的信息，正确理解项目解析根和解析别名。由于对项目配置的理解，IntelliJ IDEA为JavaScript文件中的导入和导出符号提供了更精确的代码完成。
	
	
