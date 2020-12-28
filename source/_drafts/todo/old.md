从20190601开始，准备做一些项目，提升自己。

第一步，做一个简单的博客系统，记录自己的开发过程，现已将博客系统框架搭建完成（还要改进），并发布在服务器上。

发布时遇到的问题：
1.vue 前端打包js路径。
2.前端用127.0.0.1访问不到后端项目。

--END--


结构，插件
  项目结构重新调整，使前后端项目更好的融合。
  IDEA安装一些插件，Lombok、JRebel、Vue.js、Sace Actions 以便配合插件更好的开发。
  前端项目整合axios,Element-ui。
  
前后端Long型精度不一致
- 用String 类型
- Long用@JsonSerialize(using = ToStringSerializer.class)注解


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
	

@Column 用于普通字段
@JoinColumn 用于外键字段


- ES6在语言的层面上实现了模块化。浏览器厂商和 Node.js 都宣布要原生支持该规范。它将逐渐取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。
	

eslint 文件/设置中 区别，关系
-文件：运行项目后，通过控制台才发现语法错误。
	-设置：在开发过程中，就根据ESlint规则修改代码。（不必支持项目）
		IDEA中配置：Setting ->Preferences -> Languages & Frameworks -> JavaScript -> Code Quality Tools -> Eslint ，然后勾选Enable单选框。
		
		
		IDEA webpack配置
	- 当在“设置/首选项”|语言和框架|JavaScript|Webpack中打开项目或编辑指定的webpack.config.js时，IntelliJ IDEA在后台分析配置，并根据收到的信息，正确理解项目解析根和解析别名。由于对项目配置的理解，IntelliJ IDEA为JavaScript文件中的导入和导出符号提供了更精确的代码完成。
	
	
	JPA 自定义主键生成策略
	- 继承IdentityGenerator， 不是实现IdentifierGenerator接口
- 重写generate(SharedSessionContractImplementor, Object) 方法

注：自定义生成器要有默认构造方法
	
	
	ngigx路径/结尾
	- 在某些情况下，Nginx内部重定向规则会被启动，例如，当 URL 指向一个目录并且在最后没有包含“/”时，Nginx 内部会自动的做一个 301 重定向
	- location
		- 以/结尾：url与location路径完全匹配
		- 不以/结尾：模糊匹配，以location路径开头。
	- proxy_pass
		- 以/结尾：访问服务proxy + (uri - location)路径
        - ip/域名结尾：访问服务proxy + url路径
		- 其它：访问服务proxy + (uri - location)路径 (字符串拼接，没有/)
	- root
		- 一致
	
	
	VUE conf/env '"..."'
		- JSON.parse()的语法原因，比如：JSON.parse("a")和JSON.parse('"a"')  第一个就会报错
	- 字符串变量需要包成单引号和双引号 '"..."'
	- process 对象是一个 NODE global （全局变量），提供有关信息，控制当前 Node.js 进程。作为一个对象，它对于 Node.js 应用程序始终是可用的，故无需使用 require()。
	- process.evn = conf里的 NODE_ENV
	
	
	
	vue创建项目eslint 选择/不选择
	- config/index.js
	
		module.exports = {
		  dev: {
				// Use Eslint Loader?
				// If true, your code will be linted during bundling and
				// linting errors and warnings will be shown in the console.
				useEslint: true,
				// If true, eslint errors and warnings will also be shown in the error overlay
				// in the browser.
				showEslintErrorsInOverlay: false,
			}
	
	-build/webpack.base.conf.js
	
		const createLintingRule = () => ({
		  test: /\.(js|vue)$/,
		  loader: 'eslint-loader',
		  enforce: 'pre',	// 在webpack编译之前进行检测
		  include: [resolve('src'), resolve('test')],
		  options: {
			formatter: require('eslint-friendly-formatter'),
			emitWarning: !config.dev.showEslintErrorsInOverlay
		  }
		})
		
		module: {
			rules: [	// 项目开发的过程当中，每次修改代码，能够自动进行ESLint的检查
			  ...(config.dev.useEslint ? [createLintingRule()] : []),
			]
		}
		
	-package.json
		"scripts": {
		   "lint": "eslint --ext .js --ext .jsx client/"  // 执行脚本检测
		 },
		 "devDependencies": {
			"lint": "eslint --ext .js,.vue src",	
			"babel-eslint": "^8.2.1",		// 为支持ES6语法
			"eslint": "^4.15.0",  // 代码统一风格规范 （jslint    jshint     eslint（最火的））
			"eslint-config-standard": "^10.2.1",
			"eslint-friendly-formatter": "^3.0.0", // formatter默认是stylish，vue/webpack 默认使用 eslint-friendly-formatter
			"eslint-loader": "^1.7.1",	// 用eslintrc.js配置形式使用ESLint (其它形式：.eslintrc.yaml、.eslintrc.json)
			"eslint-plugin-import": "^2.7.0",
			"eslint-plugin-node": "^5.2.0",
			"eslint-plugin-promise": "^3.4.0",
			"eslint-plugin-standard": "^3.0.1",
			"eslint-plugin-vue": "^4.0.0",
		}
	
	-.eslintrc.js  // .eslintrc 放在项目根目录，则会应用到整个项目；如果子目录中也包含.eslintrc 文件，则子目录会忽略根目录的配置文件，应用该目录中的配置文件
	
		module.exports = {
		  root: true, // 根目录，停止在父级目录中寻找
		  parserOptions: {
			parser: 'babel-eslint'	// 配置解析es6
		  },
		  env: {  // 指定代码运行的宿主环境（browser、node）
			browser: true,
		  },
		  extends: [  // 指定eslint规范
			// https://github.com/vuejs/eslint-plugin-vue#priority-a-essential-error-prevention
			// consider switching to `plugin:vue/strongly-recommended` or `plugin:vue/recommended` for stricter rules.
			'plugin:vue/essential', 
			// https://github.com/standard/standard/blob/master/docs/RULES-en.md
			'standard'
		  ],
		  // required to lint *.vue files
		  plugins: [  // 引用第三方的插件
			'vue'
		  ],
		  // add your custom rules here
		  rules: {
			// allow async-await
			'generator-star-spacing': 'off',
			// allow debugger during development
			'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
		  },
		  "globals" : {}  // 脚本在执行期间访问的额外的全局变量
		}

	-.eslintignore  // 指定不需要走eslint规范的代码 