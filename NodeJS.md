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

   

​	实例;

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

```
		
```

​	















