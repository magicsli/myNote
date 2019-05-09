# `vue`

​	`vue.js`是一个前端的渐进式框架

​		渐进式:  越学越难, ( 上手门楷低); 学啥就能用啥

​	`vue.js `是一个`mvvm`的框架

​	`vue.js` 数据也是单向的, 称之为单向数据流

​	`vue.js` 不兼容ie8及其以下浏览器

​	`MVC` 架构思维从后端引入前端: 引发了各个框架的兴起

​			

### `MVC` 模式

​		M :  model  数据      V:   View  视图      C :  Controller  控制器, ( 业务逻辑 )

​		P :  Presenter   提出者,  推荐者        VM:  ViewModel   视图模型		





​		

​	软件可以分成三个部分:   数据,  视图,  控制 相分离

​	所有的数据都是单向的

​	

​									

### MVP

+ 1, 各部分之间的通信, 都是双向的,
+ 2, View 与Model 不发生关系, 通过Presenter传递
+ 3, VIew 非常薄, 不部署任何业务逻辑, 称为'被动视图'(Passive View), 即没有任何主动性, 二Presenter非常厚, 所有逻辑都部署在哪里

​	

### MVVM

​	基本与MVP 模式一致,  ViewModle 和 View 关系更紧凑







### Vue 基础

​	**和React一样, vue也需要一个容器, 一般用root或者App 表示.引入的方法和react一致**

​	初始化一个vue实例: 

​			



​		

```
		<!-- 装载vue实例中的数据 -->
		<div id="app"> {{ this.msg }} </div> 
        
		<!-- 或者 -->
        <div id="app"> {{ this.$data.msg }} </div>
		
		<!-- 也可以简写为-->
		<div id="app"> {{ msg }} </div>
		

new Vue ({
	// 将new vue 实例装载在App这个div中, 规定了new vue处理的实例作用范围
            el: '#app',
      			
            data: {
            	msg:'hello msg'    // 使用这个数据
            }
            
		})
```



​	**new Vue( {   } )**   表示初始化一个Vue 实例

​	**el**  表示装载,  将上面id为App的模板装载在 new Vue 的实例中, 也确定了一个作用 ---- ( element )   

​	**data**  数据,  



#### 数据绑定

​	mustauch语法糖:  双大括号语法, 可以在html中的 {{  }} 写 js 语法

​	**注意:** 

+ 1, 模板中的 this 指的是 new Vue 得到的实例.  

​		在模板中我们可以省略this 

+ 2, data选项在根实例中是**对象**, 除了根实例以外,是**函数**

