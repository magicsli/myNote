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







### HTTP协议的无状态性

------

+ 1,    HTTP 协议的通信模式:  基于 `请求 - 处理 - 响应 `  的
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

 + 3,  Cookie 有一个, 每当客户端要求请求服务器了, 必然会主动携带 当前域名下所有可用的Cookie, 主动发给服务器; 客户端每次请求服务器的时候,会检查当前域名下所有可用的Cookie,并写入到

 + 4,   服务器, 也可以主动向客户端写入Cookie;

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
+ 2, 设置cookie是注意, 我们在是在请求的数据对象中设置, 对象的键名是唯一的
+ 3, 如果要设置多个cookie值,我们使用数组的形式的传参

​	

### 语法

​	`_filename`  当前文件

​	`_dirname  `    当前目录

​	





### 创建最基本的http服务器

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

  + 第一个参数是  端口号

  + 第二个参数,  是 IP 地址, 可选, 如果不填写, 则默认监听 127.0.0.1

  + 最后还有一个回调函数, 表示, 当服务器正常启动之后,调用一下这个函数

  + `server.listen(3000, function(){`

    ​	`console.log( " hello word " )`

     `} )`

+ 注意:

  + 我们自己写服务器的时候, 要时刻记着, 请求 - 处理 - 响应
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

  