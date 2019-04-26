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

​	**3, http** :   http协议模块

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
  res.writeHeaders (200, {
    "Conten-Type": "text/html; charset:utf-8"
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

  