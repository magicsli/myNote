



 # NodeJS

------

 + 附: 在学习Node之前建议先学习ES6语法

   

 ## 目标

------



+ 了解Node.js 中一些基本的概念
+ 能够使用常见的Node.js平台提供的API  
+ 能够使用`Node.js`提供的后端开发技术,  结合前端技术独立开发具有前后端交互功能的网站  - 使用Node 做后端网站

  

 ### 什么是NodeJS

------



 + 基于Chrome的V8 JS解析引擎上, 解放了 JavaScript的编程能力,为Javascript 

- 组成部分
  - ECMAScript 核心
  - 全局成员
  - 模块系统成员

### REPL环境

------



+ 如何进入REPL环境:   打开任意终端, 直接输入`node` 并回车,就会进入到REPL 环境中;
+ 如何离开REPL环境, 按两次`ctrl + c` 就能退出REPL环境
+ REPL 中, 每个字母代表什么意思呢;
  + R :   Read的意思 , 每当我们输入完毕代码之后, 只有敲击回车, node环境就会读取用户输入的代码
  + E :   Evaluate 的意思,    表示吧Read进来的用户代码, 调用类似Eval 的函数, 去解析执行
  + P :   print 输出的意思, 把第二步中解析执行的结果,输出给用户;
  + L :    Loop循环的意思,  表示当输出完毕之后, 进入下一次的REPL循环

### Node 命令(推荐形式)

------

- node   指定的文件名
  + node为JS 提供了一个,脱离浏览器平台,也能被解析执行的环境



### 前端模块化

+ 1,  CMD     ( sea.js )
+ 2,  AMD     (  require.js  )
+ 3, Common.js
+ 4,  es6 模块化

CMD 和 AMD 

​	define 定义模块

Node.js中使用了common.js规范 (三类)

+ 1,  内置的
+ 2,  第三方的
+ 3,  自定义的 



#### Node.js 内置了很多的模块

+ fs ( 文件系统 )
+ path ( 磁盘路径 )
+ http ( 通信 )



##### 使用

+ 1, 导入
  + `const 变量名称 = require( "模块名称" );`
+ 2,  使用模块的api
  + path.resolve( _dirname )   // 获取当前文件的目录路径

#### 在Node.js中使用第三方模块:   http:// www.npmjs.com

+ 1,  安装
  + 1,  初始化生成 package.json       命令:     ` npm  init  -y`
  + 2,   安装对应的包;      命令:      `npm  i request -D / -S / -g`
    + -g     -global   全局
    + -D   /  --save-dev   开发环境
    + -S   /   -save   生产环境
+ 2,  导入
  + request  用来做数据请求的
+ 3,  使用
  + 文档天下第一,什么视频教程全是虚的



`const` request = require("request")



**Node.js 中请求数据, 需要跨域么?:**

​	**因为node是在服务器环境下运行**  

​	由于node的运行环境不是浏览器,所有不存在**同源策略**的限制

同源策略

+ 1,  为什么会出现跨域
  + 开发中会有不同的**域名**和**端口**等出现, 我们需要去获取他们的内容
+ 2,  浏览器如何组织跨域
  + **浏览器**具有安全策略  -->    同源策略实现
+ 3, 跨域的范围是:
  + 浏览器

#### package.json的作用

​	分析:  帮助我们记录第三方的内容, 即使我们没有node_modules也可以下载

****



#### 前端的环境

+ 1, 开发环境

+ 2, 生产环境

+ 3, 测试环境

+ 4, 预发布环境

+ 5, 上线环境

  

#### 自定义模块的步骤

+ 1,  定义

  + 对象,  函数,  字符串  ....

+ 2, 导出

  + module.export || reports

  + reports 是 module.exports 的一个辅助工具

  + 在 node 导出需要加一个 = 号

  + 基于安全性考虑, 建议封装一下:

     	//  让请求此模块的文件不能修改

    ```
    module.exports = {
        age: age.age,
        name: age.name
    }
    ```

    

+ 3, 使用

  + const 变量名  = require( ''模块名" )

  注意:  使用自定义模块是需要加路径

  - const  变量名 = require ("./module/模块名")

    

+ 4, 自定义模块的发布: 

  + 封装好包
  + 在 http://www.npmjs.com 上发布
  + 操作流程:
    + package-lock.json  ===> 当前项目依赖包的具体信息
    + 确定当前的源是npm的源, 
    + npm adduser  注册用户信息(与npmjs账号上一致)
    + npm publish  发布

  

node.js  是单线程

​	主线程

​	异步队列: Node.js 中异步任务, 放在异步队列

​	注意: 优先执行主线程中任务吗主线程任务结束后,再运行异步队列任务





### 包的导入规则

+ 当我们导入一个包的时候,会先在包的根目录中, 查找一个叫做"package.json"的文件
+ 如果有"package.json"文件, 则会继续查找这个文件中的,一个叫做"main"的属性
+ 如果能找到"main"属性, 则尝试加载 "main"属性所指向的那个文件
+ 如果这个文件,加载成功, 则这个包,就已经被正常require进来了,就可以正常使用了



### 自定义包

+ **包都有以一个单独的目录而存在**
+ **`package.json `必须在包的顶层目录下**
+ **`package.json`文件必须符合JSON格式, 并且必须包含如下三个属性: `name`, `version`, `main`**
  + `name` : 包的名字
  + `version`: 包的版本号
  + `main` :表示包的入口文件
+ 二进制文件应该在**bin目录**下
+ javaScript代码应该在**lib目录**下
+ 文档应该在**doc目录下**
+ 单元测试应该在**test目录**下
+ Node.js对包要求并没有那么严格, 只要顶层目录下有`package.json`, 并且符合**基本规范**即可

### HTTP协议的无状态性

------

+ 1,    HTTP 协议的通信模式:  基于 ***`请求 - 处理 - 响应 `***  的
+ 2     由于这个通信协议的关系, 导致了HTTP每个请求直接是没有关联的, 每当一个请求完成之后, 服务器就忘记之前谁曾经请求过
+ 3,    如果纯粹基于HTTP 通信模型, 是无法完成登录状态保持的!   每次请求服务器,  服务器都会把这个请求当作新的请求来处理!
+ 4,    我们可以通过cookie 技术, 实现状态保持,  但是由于cookie 是存储在客户端的一门技术, 所以安全性几乎没有, 因此不要使用cookie存储敏感的数据!





## Cookie

------

### 什么是cookie, 作用是什么

​	由于 **  HTTP协议是无状态的 ** , 且传统服务器 ** 只能被动的响应请求 ** , 所以. 当服务器获取到请求的时候,  并不知道当前的状态,所以需要一个东西来记录状态值,cookie就是这个记录的文件





### Cookie的特性

 + 1,  是专门用来在服务器端和客户端之间传递一些文本数据的, 从而用来记录客户端的身份

 + 2, Cookie的本质, 是一段小文本;

 + 3,  Cookie 有一个, 每当客户端要求请求服务器了, 必然会***主动携带*** 当前域名下所有可用的Cookie, 主动发给服务器; 客户端每次请求服务器的时候,会检查当前域名下所有可用的Cookie,并写入到

 + 4,   服务器, 也可以***主动***向客户端写入Cookie;

 + 5,  cookie 是不安全的,  因为cookie存放在客户端浏览器中, 容易被篡改;

 + 6,   使用 res.writeHeader,  指定Set-Cookie 来向客户端写入Cookie, 如果写入多个,  则值应该是一个数组




### 设置Cookie实例:



​	const  http = require('http')

​	const server = http.createServer()

server.on("request", (req, res)=>{

res.writeHeader(200, {
            "Content-Type" : 'text/html; charser=utf-8',
            'Set-Cookie': ['isvisit=yes' ,  ' name=zs']
		})

​	res.end("送你一朵小红花")

})

server.listen(4000, ()=>{

​	console.log("服务器运行在 http:// 127.0.0.1:4000")

})



#### 设置cookie的注意点

+ 1, `cookie`在 `res.writeHeader `中设置, 在请求头中设置的cookie
+ 2, 设置cookie是注意, 我们在是在请求的数据对象中设置, 对象的键名是***唯一***的
+ 3, 如果要设置多个cookie值,我们使用数组的形式的传参

​	

#### 如何获取`cookie`

+  `req.headers`  请求的请求头数据中就有cookie的数据
+ 获取cookie  -    ` req.headers.cookie `





### 语法

​	`_filename`  当前文件

​	`_dirname  `    当前目录

​	





### 创建最基本的http服务器

​	使用node.js实现一个web服务器,    (API服务器)

​	node.js中模块的api很多时候可以连缀(链式调用)



​		// 格式:    http.createServer(callback).listen(prot, hostname, callback)

```
require("http").createServer( function (request, response) {
		response.writeHeader(200,{
            "Content-Type": "text/html; charset=utf-8"
		})

		response.write("yanyabing"); 

		response.end()   // 结束发送

}).listen(port, hostname, function(){

		// 在后端控制台输出

})

```

​	

###**3, http** :   http协议模块

+ 1, createServer  创建一个web静态服务器

+ 2, listen    是用来监听服务器

+ 3, 名词解释:

  + 1, port  端口
  + 2, hostname  域名
  + 3, request  请求
  + 4,  response  回应
  + 5,  data   数据
  + 6,   encoding  编码方式  utf-8 

+ 4, `write (data,  encoding)`  给前台发送一个内容

+ 5,  `end()`发送已经结束了

+ 6, 中文会乱码, 需要设置请求头

  ```
  res.writeHead (200, {
    "Conten-Type": "text/html; charset:utf-8"
  })
  
  ```

+ 7, get 服务器请求其他域的资源:

   

  ```
  require("http").get("http://www.baidu.com/index.html?da=12" ,  function(res) {
      
        
  })
  ```

  

  #### 服务器常用模块 

  ####URL

  + 用来做浏览器  地址  解析
  + 完整的url 构成
    + https://  www.magicsli.com :80 /vue/index.html  ?name=123&code=456#x=12
    + 协议:  https
    + 域名:   www.magicsli.com 
    + 端口:  : 80
    + 路径:    www.magicsli.com :80 /vue/index.html
    + 查找字符串:   ?name=123&code=456
    + 哈希:   #a=10

  ##### API

  ​	parse :  String ==>   Object         将URL中的字符串数据 转换为**对象**

  ​	format:  Object  ==>  String	将对象转换为字符串   与上一个相反

  ​				-  注:    %20 代表空格

  ​	resolve   url 拼接    url重定向

  ​	url.resolve( url, "新的路径" )



#### query string

​	进行string 和object 的格式转换

类似于JSON.parse   ||    JSON.stringify

##### API

​		parse 

​		stringify      Object  ==>   string   用来解析对象来传递url后中的参数

​		escape       将文本进行编码

​		unescape     解码,  



### fs 文件模块

​	**读文件** 

​	  ` require("fs").reafFile("文件路径" ,  (err, data) => {`

​		`err && console.log(读取文件出错);`

​		`data  &&   console.log(data)`

`}  )`

​	

​	**写入文件**

​		

```
require("fs").writeFile("路径+文件名", "文件内容" ,"内容类型", (err)=>{
    if(err) {
        console.log("写入文件错误")
    }
} )
	
```

​	

​	**给文件增加信息**

require("fs").appendFIle("文件路径" , "要增加的数据 ", "参数", 错误回调函数)

​	注意, 如果文件不存在,会自动创建一个新的文件,并执行增加数据的操作





​        **读取文件信息**

​	fs.stat

​		





### path

​	`path.sep `  **提供指定平台的路径片段分隔符**

​	`path.join() `  **拼接路径**  

​			`path.join(__dirname, "/file/01.text")`



​	**读取文件目录 **   `dirname`

​		`fs.readdir(__dirname, (err, filenames) => {`

​		`console.log(filenames)	`

​	`})`

​	

​	**读取文件名**  ` basename`

`

​	**获取文件后缀**  `extname`







### events事件模块

​	请求 :   const EventEmitter = require("events");

class MyEmitter extends EventEmitter { }

const myEmitter = new MyEmitter();



​	只执行一个的事件监听器

​	Emitter.prototype 继承过来了 on emit



### Stream

​	读取文件流

​	可读流的事件

​	可写的文件流

​	pipe的链式使用

​	pipe





### zlib 压缩包模块

​	制 作一个压缩包的步骤:

+ 先有一个文件
+ 读取文件  // 必须以流的形式
+ 制作压缩包
+ 将读取的数据放入压缩包中

```
const zlib = require('zlib');
const fs = require('fs');

	// 创建可读的流
	const inp = fs.createReadStream('yyb.txt')
	
	// 创建空压缩包
	const gzip = zlib.createGzip()
	
	
	// 创建可写的流
	const out = fs.createWriteStream('yyb.txt.gz')
	

inp.pipe(gzip).pipe(out)
// pipe 管道流 

```











![http通信模型](C:\Users\25445\Desktop\http通信模型.png)

+ 导入Node中提供的核心模块 http

  + `const http = require("http") `

+ 创建服务器

  + `const server = http.createServer()`

+ 为这个server服务器, 通过 on 方法, 绑定一个事件

  + `server.on("request")`    -- 绑定一个请求事件
  + 问题:  这request 事件什么时候出发
  + 回答:  每当服务器接收到一个客户端的请求, 就会立即触发这request事件

+ 启动服务器

  + 第一个参数是  ***端口号***

  + 第二个参数,  ***是 IP 地址***, 可选, 如果不填写, 则***默认监听 127.0.0.1***

  + 最后还有一个回调函数, 表示, 当服务器正常启动之后,调用一下这个函数

  + `server.listen(3000, function(){`

    ​	`console.log( " hello word " )`

     `} )`

+ 注意:

  + 我们自己写服务器的时候, 要时刻记着, ***请求 - 处理 - 响应***
  + 在服务器的回调函数列表中 ,有两个参数, 其中,第一个参数, 是Request,  第二个参数是 Response 

+ `server.on("request", function(req,  res) {`

  ​	`console.log( " ok " )`;

  ​	`res.end( "` ***这是服务器返回的数据*** `" )   `

   //  响应, 就是返回给客户端的数据. 类似于php的 echo

  // 每次请求处理完毕, 必须显示调用一下 response 对象的end 方法; 来结束这次响应, 否则, 客户端拿不到数据

  `})`

+ 获取浏览器请求的url地址:

  + `req.url`
  + 服务器获得url地址以  `/`   开头
  + 如何拿到请求的类型:
    + `req.method.toLowerCase()`
  + 每当有客户端来请求服务器, 我们服务器, 直接把请求的类型和请求的url地址, 拼接成字符串给客户端显示
    + res.end("请求的类型是:" +req.method+"请求的URL地址是"+req.url)

  

+ 设置返回响应头:

   	`res.writeHeader(200, {`

  ​		"`Content-Type" : "text/html; charset=utf-8`"

  ​	`})`

  - 第一个参数, 是数值类型的状态码,  200 成功,   300 重定向,  404 资源找不到,    500 服务器内部错误
  - 第二个参数是一个配置对象:
    - Content-Type 的值有   
      - text/html     
      - text/plain
      - image/jpg
      - image/png
      - image/gif
    -  注意格式,格式必须一致

  ​	

+ 根据请求类型判断返回数据:

  ​	

  ```
  server.on("request", function(req, res){
      if(req.method === "POST" && req.url === "/home" ){
          res.end("您访问的类型是POST")
      }
      
  })
  ```

+ 根据请求返回页面

  + 注意: res.end() 只接受字符串和Buffer二进制的参数
  + 需要先把html文件用readfile解析, 再通过res.end()返回
  + 需要用到fs模块和path模块     代码:

  ```
  const http = require("http")
  const fs = require("fs")
  const path = require("path")
  const server = http.createServer()
  server.on("request", (req, res)=> {
      fs.readFile(path.join(_dirname, "/views/index.html"),   "utf-8", (err, data) => {
          if(err) return res.end("404")
          res.end(data)
      }
  })
  ```

  





### 模块

+ require  请求模块, 类似于 import 

+ module.export    导出模块  类似于 export:

  +  module.export.xxx = xxx ; 导出xxx

  + 我们一般采用  moudle.export = {

    ​	 xxx = xxx,

    ​	 yyy = yyy

    } 

  







## Express 框架

+ 基于Node.js后端javascript平台之上开发的一套web开发框架

+ Express中, 基于原生node的特性, 做了进一步封装,提供了一些更好的方法,提高web开发的体验

+ Express中, 并没有删除了覆盖原生的http方法

  ------

  

1, 安装生成器: 

​	`npm i express-generator -g`

2, 使用

​	`express options 项目名称`

3, 创建项目

​	`express newProject`

4,  目录内容

​	bin		     ==>     项目的配置文件  ( 比如:  port )

​		 --    www         使用 http 模块创建了一个web服务器

​	public		==>     静态资源文件夹 ( html  css  images  js )

​	routes	        ==>    后端路由文件夹  -->   express 提供的路由模块

​	views	         ==>    后端模板文件夹

​	app.js	        ==>     整个项目的入口文件

​	package.json     ==>    整个项目的依赖包配置文件

5, 项目启动:

​	1, 进入项目	`cd 项目名称`

​	2, **安装项目需要的依赖**	`npm install`                     ---  注意, 这步不能缺少

​	3, 项目启动(说明书:  package.json 中 scripts 脚本)    `npm start`

**建议**: 拿到一个项目,先看他的`package.json`文件



6, 看一个项目流程

​		1,  package.json

 			依赖包

​			npm 脚本  ==>  项目启动命令  ==>  配置文件



7 express 中间件    middleware

​	中间件:具有特定功能的插件

​	express 中提供了

​		1, 应用级中间件

​			生成    `const  app = express( )`

​		使用:

​			1, app.use()

​			2, app.method()  处理`http`请求

​	应用级中间件就是一个具有特点功能性的函数, 这个函数需要绑定在app对象身上, 通过`app.use() || app.method ()`来调用



**请求方式:**

​	比如: `get`   `post`  

​	**`delete`**    (删除请求) 

​	**`put`**          (添加请求) 

​	 **`all`**         (所有请求)





​		2, 路由中间件

​			

​		3, 错误中间件



##### Node.js 的渲染引擎有哪些

+ ejs
+ pug
+ art-template



####express使用案例:

​	

```
var express = require("express");
var App = express();

app.get("/",  function(req, res){    // 这点可以作为路由操控
    res.end("hello  word");
})
var server = app.listen(3000, function(){	

var host = server.address().address;

var port = server.address().port

})

```

​	

####API

**`app.get()`  监听get类型的请求**

**`app.post( )`监听post类型的请求**

**`app.all()`	监听所有类型的请求**

**`app.send()`       类似于原生的`end()`可以解决中文乱码的问题**



+ 通过调用 `express()`   可以得到一个`express `服务器
+ app.get     app.post      app.all      app.listen
+ res.send      res.sendFile
+ 利用Express托管静态文件  `express.static`          这是一个express的内置中间件
  + 将静态资源文件所在的目录作为参数传递给express.static中间件就可以提供静态资源文件的访问了, 例如, 假设在public目录放置了图片, css和javaScript文件
  + `app.use(express.static("public"))`
  + 当使用第二步中的方法, 把指定目录托管为静态资源目录之后, 那么, 这一层被托管的目录, 不应该出现在资源访问的url地址中
  +  在一个web项目中, 我们可以多次调用此方法
  + 注册一个虚拟目录: 
    + `app.use("/static", express.static("public")) `
    + 为这个静态托管注册了一个虚拟目录
+ 资源压缩中间件:   `app.use(compression())`
  + 下载包:   npm i compression -S`
  + 引入:     ` const compression = require("compression")`
  + 使用:      `app.use(compression())`
+ `express`中的`result`方法:
  + `res.sendFile` 只能提供静态文件, 不能渲染动态页面
    + `res.sendFile(path.join(__dirname, "/test.html"))`
  + `res.render(path, data)` 渲染函数
    + 参数1 `path`  要渲染的页面名称
    + 参数2 `data`  要渲染的数据对象
    + 注意默认情况下, 我们无法直接使用res.render函数来渲染动态页面, 因为express并没有为我们提供默认的模板引擎
    + 所以, 在调用`res.render()`函数之前,我们要先人为的值定使用哪个模板引擎来渲染页面
      - 配置模板引擎 :
        - 1 安装合适的模板引擎      运行   `npm i ejs -S`
        - 2, 配置模板引擎           app.set( "view engine", "ejs" ) 第一个参数是固定写法,   第二个参数是模板引擎的类型
        - 3,配置模板引擎的存放路径     app.set('views', './views') 第一个参数是固定写法,   第二个参数是模板页面的存放路径
    + 调用 `res.render("index.ejs", person)`

+ 路由

  + 前端请求的url地址必然对应一个后端的处理函数

  + 后端的路由, 主要用来分发请求的

  + 请求- 处理- 响应

    代码:

    ```
    const router = express.Router();
    
    const person1 = { data:123333 };  // 数据对象1
    const person2 = { data:123333 };  // 数据对象2		
    const person3 = { data:123333 };  // 数据对象3
    
    router.get("/demo1", (req, res) =>{
        res.render("index", person1)
    })
    ```

    router.get("/demo2", (req, res) =>{
        res.render("index", person2)
    })

    router.get("/demo3", (req, res) =>{
        res.render("index", person3)
    })






### KOA  

​	**koa是express超集(就是express的进阶版)**





 



1, webServer

2, apiServer (后端工程师, 前端写接口) ==>  测试工具  ( postman )

​	1, express     ==>     一个路由就是一个接口

​	2, koa  	

3, MongoDB(命令) ==> 连接数据库, 操作数据库  ==> mongoose

4, gulp搭建项目( 跨域 )



接口示例:

​	

```
const express = require("express");
const router = express.Router();
router.get("./position", function(req, res, next){
    res.render('position', {msg:"hello word"})
})


module.exports = router




/* 在模板文件中*/
	/*  position.ejs  */
	<% !--- js语法 --- %>
	
	
	
```



玩架构思想:

​	**RMVC**

​		R	==>	`Router`路由

​		M	==>	`Model`路由

​		V	==>	`VIew`视图

​		C	==>	`Contriller` 控制器( 逻辑 )

