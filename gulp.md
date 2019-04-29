

#gulp 4.0



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
+ 

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

```

```

​	





