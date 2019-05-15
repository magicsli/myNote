##  `nrm`的安装的使用

------



#### 作用:

 



​		提供了一些最常用的 `npm` 包镜像地址,能够让我们快速的切换安装包时候的服务器地址;

#### 什么是镜像:

 

​		原来包刚一开始只存与国外的`npm `服务器,但是由于网络原因,经常访问不到,这时候,我们可以在国内.创建一个和官网完全一样的`npm`服务器,只不过,数据都是从人家那里拿过来的,除此之外,使用方式完全一致

1,  运行`npm i nrm -g`全局安装`nrm`包;

2,  使用`nrm is`查看当前所有可用的镜像源地址以及当前所用的镜像源地址;

3,  使用`nrm use npm `或 `nrm use taobao`切换不同的镜像地址

​	 

> > > > > > 注意: `nrm`只是提供了几个常用的 下载包的`url`地址,  并能够让我们能够在这几个地址之间,很方便的进行切换,但是,我们每次装包的时候,使用的装包工具,都是 `npm`







##`webpack`的学习与使用

------



#### 在网页中会引用哪些常见的静态资源

+ `JS`

  - `.js`  	``jsx`	`.coffee`	`.ts(typescript)`		

+ `css`

  + `.css` 	`.less`	`.sass`	`.scss`

+ `IMages`

  - `.jpg`	`.png`	`.bmp`	`.svg`

+ 字体文件(Fonts)

  + `.svg`	`.ttf`	`.eot`	`.woff`	`.woff2`

+ 模板文件

  + `.ejs`	`.jade`	`.vue`这是在`webpack`中定义组件的方式,推荐这么用

    

#### 网页中引入的静态资源多了以后有什么问题

------

​	1, 网页加载速度慢, 因为我们要发起很多次的二次请求

​	2, 要处理错综复杂的依赖关系



####  如何解决上述问题

------

1, 合并, 压缩, 精灵图, 图片的`Base64`编码 (减少二次请求, 提高加载速度)

2, 可以使用`requireJS` , 也可以使用`webpack`可以解决各个包之间的复杂依赖关系



#### 什么是`webpack`



------

​	`webpack` 是前端的一个项目构建工具, 它是基于 `Node.js` 开发出来的一个前端工具;

+ 资源打包工具
+ 可以解决模块化依赖问题
+ ES6模块化









### 前端环境

+ 开发环境

+ 生产环境

+ 测试环境

+ 预发布环境

+ 上线环境

  

   - 开发环境  和  生产环境   都是有前端静态服务器来提供

   - 测试环境   本地客户端服务器提供

   - 预发布和上线环境是  nginx    

     



#### webpack.config.js配置

+ 1, 单页面

  + 入口文件   **相对路径**

  + 出口文件   **磁盘路径**

    + 为什么要配置hash 

      + 保存上一个版本的信息, 不进行文件的覆盖

    + 配置hash

      ```javascript
      output:{
          path:path.join(__dirname, dist),
          filename: 'js/main_[hash:6].js'
      }
      ```

  + 转换器:  将某一类型的文件转成另一类型文件的一个工具, 我们常用loader来表示

    -- 在`webpack`中, 所有其他类型的文件全部要转化为js文件

     

    + css      // css模块文件
    + css-loader   // sass模块的加载器所有的loader用一个module的配置项表示

    ```javascript
    module:{
        rules:[
            { //每一个对象表示一个类型文件的转换器
                
                // 检索所有后缀为.css文件
                test: /\.css$/, 
                // 使用数组中的加载器进行加载, (css)
                use:['style-loader', 'css-loader'] 
            } 
        ]
    }
    ```

    

+ 多页面

  ​	entry写成对象, 代表多个入口

  - 修改入口文件 使用对象
  - 修改出口文件   使用 [ name ]

  ```javascript
  module.exports = {
      entry:{  // 多页面
          // 入口文件的名称 : 入口文件的路径
          index: './src/index.js',
          app:'./src/app.js'
      },
      output: {
          path: path.resolve(__dirname, 'dist'),
          filename:'js/[name].js'
      }
  }
  ```

  

+ 自动解决模块依赖问题 









































####  如何完美事项上述的俩种解决方案

------

1, 使用` gulp`     - 是基于 `task` 任务的

2, 使用`webpack `	- 是基于整个项目进行构建的

+ 借助于`webpack`这个前端自动化构建工具, 可以完美的实现资源的合并, 打包, 混淆等诸多功能.

+ 根据官网的图片介绍`webpack`打包的过程

+ <a href="http:// webpack.github.io">[webpack官网]</a>

  

  

#### `webpack`的安装与使用

------

​	1, 运行`npm i webpack webpack-cli -g`全局安装`webpack`,这样就能在全局使用`webpack`中的命令

​	2, 根据项目目录中运行`npm i webpack --save-dev`安装到项目依赖中,

​		如果版本是4.* .* 就要安装` webpack-cli` :

​			`npm install webpack-cli --save-dev`

### 举个例子:

​	

+ 我要导入一个script ,除了以前的`src`引入 ,现在用`webpack`试试;
  + 1,   准备项目 :
    + `npm  init -y`		-- 注意: 这里如果用`npm`就不用yarn,  俩者会合并,可能带来不必要的bug
    + `npm install webpack webpack-cli --save-dev`        -- 下载依赖包`webpack`
    + 创建 `webpack.config.js` 文件           --这是`webpack`的配置文件  -- 目前不会用到,在配置中使用
    + 调整`package.json`文件, :
      +  在配置中删除这一段, 我们不需要这句 "`main`" : "`index.html`" 
      + 将配置文件设置为私有,防止意外发布代码  "`private`" : `true`;  放在刚才删除的地方
    + 创建一个包, 捆绑 `lodash`  依赖项 `index.js`     :
      + `npm install --save-dev lodash`
    + 在`js`中导入 -   import   _ form ' lodash'
    + 将我们的`HTML`中的src都去掉
    + 引入一个 `main.js` 标签
    + 运行` npx webpack`  '.`/src/index.js`'   '`./dist/main.js`'



## 使用配置

------

​	在我们之前创建的` webpack-config.js`中我们可以手动进行配置. 

  + 注:    	在版本4 .* .* 的时候,才开始, 在4.0.0之后`webpack`不需要任何配置,但是大多数项目需要更复杂的配置,所以`webpack`支持配置文件,这比手动输入命令行要舒服的多:

#### 示例



​		

```
const path = require('path');				--创建一个常量请求path

moudle.exports={							--引出模块配置
    entry  : './src/index.js',				-- 设置入口
    output : {								-- 输出
        filename:'main.js',					-- 文件名   main.js
        path:path.resolve(__dirname, 'dist')   -- 设置路径 放在目录名 dist 之下
    }
};
```





## `npm`脚本

------

从`cli`运行`webpack`的本地副本太麻烦; 所以我们可以有个快捷的方法: 添加一个`npm `脚本来调整我们的`package.json`

​	在   "script" : {

​	删除	-         ` "test" :  "echo \ "Error:  no  test   specified\" && exit 1 ",`

​	增加	+	`"test":"echo \ "Error:  no  test   specified\" && exit 1 ",`

​	增加	+	`"build":"webpack"`

}		



####现在`npm run build`可以使用该 `npx`命令代替我们之前使用的命令. 请注意,  `script`我们可以按照与之相同的方式引用本地安装的`npm`软件包,  



### 导入一些`css`文件试试

+ 下载 `style-loader  ` 和  ` css-loader` 工具包:     `npm install --save-dev style-loader css-loader`

  + 我们需要这些加载器来加载我们的`.css`文件以及`style`的

+ 在`webpack.config.js`中添加一个模块功能:

  + ```
    moudle : {        -- 增加一个模块功能  用来引入.css文件并且解析style  -- 这个只需要创建一个就好了时
          rules: [	  --  设置规则
              {
                  test :/\.css/,   -- 检验文件后缀
                  use:[			   -- 设置加载器插件
                      'style-loader',  -- 加入style-loader插件
                      'css-loader'	   -- 加入css-loader插件
                  ]
              }
          ]
        	
    }
    ```



### 加载图片

+ 下载文件加载器 ( ` file-loader`  )    	` npm install --save-dev file-loader`

+ 在`webpack.config.js`中加入此引入图片的模块功能

    	

  ```
  moudle : {     -- 增加一个模块功能 用来引入图片格式的文件
      rules:[		-- 设置规则
          {
              test:/\.(png|svg|jpg|gif)$/,   -- 检验文件后缀
              use:[						   -- 设置要使用的插件
                  "file-loader"			   --  引入文件加载插件
              ]
          }
      ]
  }
  ```

  



​	

##`Webpack` 命令行流程：

1.	Webpack 命令行流程：
   1.	cnpm init
   2.	cnpm i webpack -d
   3.	cnpm i webpack-cli -d
   4.	cnpm i webpack-dev-server -d
     	需要在package.json 配置：“dev”:”webpack-dev-server”
   5.	cnpm i html-webpack-plugin -d 
     	需要在webpack.config.js 配置 插件
   6.	cnpm i jquery less -dev
     	根据需要下载一些第三方的 loader 和依赖项
   7.	cnpm i css-loader style-loader less-loader url-loader file-loader -d
     babel 模块：
   8.	cnpm i babel -d
   9.	cnpm i babel-loader -d
   10.	cnpm i @babel/core @babel/cli @babel/preset-env -d
     	引入babel的预设包，加载一些es6 or es7新的模块，语法
   11.	cnpm i @babel/plugin-transform-runtime -d
      	引入babel插件， 转换工具
   12.	cnpm i @babel/runtime @babel/plugin-proposal-function-bind -d
      	函数插件，其中@babel/plugin-proposal-function-bind就相当于stage-0
   13.	cnpm i @babel/plugin-proposal-class-properties -d
      	类插件，解析类的语法
   14.	npm run dev





##`webpack` 的概念

------

### 入口

   + 入口起点 ( `entry`) 指示  `webpack` 应该使用哪个模块, 来作为构建其内部依赖图的开始, 进入入口起点后, `webpack` 会找出有哪些模块和库入口起点( 直接和间接 ) 依赖的.

   + 每个依赖项随即被处理, 最后输出到称之为 `bundles` 的文件中, 我们将在下一章节详细谈论这个过程

   + 可以通过`webpack`配置中配置 `entry` 属性,  来指定一个入口起点(或多个入口起点). 默认值为 `./src `

       	

     ```
     module.exports = {
         entry: "./path/to/my/entry/file.js"
     };
     ```

     



## 出口

+ `output`属性告诉`webpack` 在哪里输出它所创建的`bundles`, 以及如何命名这些文件, 默认值为`./dist`  基本上,整个应用程序结构, 都会被编译到你指定的输出路径的文件夹中. 你可以通过在配置中指定`output` 字段, 来配置这些处理过程.

  ​	

  ```
  const path = require('path');
  module.exports = {
      entry:"./path/to/my/entey/file.js",
      output:{
          path: path.resolve(_dirname, 'dist'),
          filename:"my-frist-webpack.bunle.js"
      }
  };
  ```

  

## loader

​	设置加载器, 可以处理  `webpack`  的配置中 `loader` 有两个目标:

​			1,` test `属性, 用于标识出应该被对应的 `loader` 进行转换的某个或某些文件

​			2, `use` 属性,   表示进行转换时,  应该使用哪个 `loader`

​	

```
	const path = require("path");

	const config = {
  	  output: {
 	       filename:'my-first-webpack.bundle.js'
 	   },
 	   module:[
 	       rules: [
  	          {
  	              test:/\.text$/, use:'raw-loader'
 	           }
 	       ]
  	    ]
	};


	module.exports = config;
```

