

#gulp 4.0

​	**构建工具**

​		1>  合并文件

​		2>  压缩与混淆

​		

操作流程:

​		1, 下载依赖gulp

​		2, 创建**`gulpfile.js`**文件

 			在该文件中写任何代码都是gulp去处理文件的代码

​			gulpfile文件提供的是一个载体, 只实现需要处理什么文件 ,保存到哪个地方等功能

​		3, 在`gulpfile`中要使用`gulp`就需要**把`gulp`引进来**

​			`var gulp = require("gulp")`   // 引入gulp模块

​		4, gulp 需要创建任务

​			`gulp.task('任务名', function(){`

​				// 执行对应的任务就是在执行这个函数 

​			`})`

​		5, 执行任务:     **gulp  任务名**

​		6, 在gulp中有一个**默认**的任务: **`default`**

​			

```
			gulp.task('default', function(){
				console.log("默认任务开始")
			})
```

​			**注意:** 

​				gulp本身只提供平台, 他不做任何事项, 需要使用**插件**来完成其他事项

​				<a href="gulp.js.com/plugins">官方的插件地址</a>   --- 文档不完整, 不建议

​				<a href="www.npmjs.com">npmjs官网</a>	   ----   推荐

gulp的插件前缀是gulp  :

​		`gulp-concat`	(连接文件)	

​	

#### gulp-concat合并文件

​				

**用法**:

​	

```
	var concat = require("gulp-concat");

		gulp.task('script' , function(){
	
		return gulp.src('./lib/*.js')

			.pipe(concat('all.js'))

			.pipe(gulp.dest('./dist/'));

	})

```

​	**但是这种合并文件会要文件的默认排序进行默认拼接,如果有优先级限制,肯会报错**



## 注意:

​	**在创建任务时, 如果不加return就是异步进行, 如果加了return就是同步任务**



```
	var concat = require|("gulp-concat");
	
	gulp.task('script', function(){
        return gulp.src(['./lib/file3.js', './lib/file1.js, './lib/file2.js'])
        .pipe(concat("bundle.js"))
        .pipe(gulp.dest('./dist/'))
	})
```

​	**这样设置就会按照数组的顺序进行拼接合并**





#### gulp-uglify 压缩文件模块



```
var press = require("gulp-uglify")

gulp.task('press', function(){
    gulp.src('/dist/*.js)
    	.pipe( press() )
    	.pipe( gulp.dest('./dist/') )
})
```



#### 构建多个任务



​	// **先执行数组中所有的任务, 待任务执行完成之后,来执行当前task在的任务**



```
gulp.task("任务名", ["任务名", "任务名", "任务名"], function(){
    //***
})
```



gulp 当前完成的任务:{

 	1, 启动webserver

​	 2,  编译sass,  less

​	 3,  CommonJs模块化

​	 4,  Mock数据

​	 5,  在Gulp 里应用babel



}

**gulp 4.0**最大特点: 

+ 增加了串行和并行的概念
  + series()  并行
  + parallel() 串行

**用法**:

+ 引入gulp
+ 引入插件
+ 利用插件定义任务
+ 监听整个项目
+ 执行任务

  

​	





安装:

+ `npm i gulp -D`
+ npm i gulp-webserver -S ( 已经改名了 )
  + npm install gulp-connect -D   (推荐)

 

var  gulp = require("gulp"),

​	connect = require("gulp-connect");



**gulp 3.x 执行任务**

```
	gulp.task("default", ["server"], function(){

	console.log("task is done~~~")

} )

```

**gulp 4.x 执行任务 **  使用**串行**和**并行**



**series串行**

```
const {series, parallel } = gulp 

gulp.task("default" , series(["server"]), function(){
    
    console.log("task is done~~~")
})

```

​	





