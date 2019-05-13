# `vue`

​	`vue.js`是一个前端的渐进式框架

​		渐进式:  越学越难, ( 上手门楷低); 学啥就能用啥

​	`vue.js `是一个`mvvm`的框架

​	`vue.js` 数据也是单向的, 称之为单向数据流 // 只用input是双向数据流

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

+  



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



`/* 行内的指令:   v-***   `



` v-for = " item in arr " `			    循环

`v-if` = " msg " 			  			   条件

v-else 					  			 否则 ( 配合`v-if`使用 )

`v-else-if` = " /// "		      	 		再进行条件判断

`v-bind:title = "我是绑定"`			    绑定( title属性 )

`v-on:click = " 事件处理函数 "`		     绑定监听事件 

`v-model = "message"`			这个类型与自动化的react中的自动化受控组件, 只需要在input中输入参数,其data中的状态值也会发生改变









`*/` 





#### 数据绑定

​	mustauch语法糖:  双大括号语法, 可以在html中的 {{  }} 写 js 语法

​	**注意:** 

+ 1, 模板中的 this 指的是 new Vue 得到的实例.  

​		在模板中我们可以省略this 

+ 2, data选项在根实例中是**对象**, 除了根实例以外,是**函数**





#### Vue 的底层代码

------

​	**Vue是一个匿名函数**

+ 1, 确定了 vue库的用法
     + 直接将vue当作全局的一个方法使用,因为将Vue挂到了window
  + 使用了amd 来定义vue.js这个库为一个模块, 这样我们才能模块化引入

+ 2, 封装库如何定义  : 例:

  ​	

  ```
  (
  	function(){
          typeof exports === 'object' && typeof module !== 'undefined' ? module.exports = factory();
          
          typeof define === 'function' && defin.amd ? define(factory);
          
          (global = global || self, global.Vue = factory() );
  	}
  
  )(this, function(){
      'use strict'
      
      function Yyb () {
          console.log('this is a demo')
      }
  })
  ```

  

### `mustache`模板语法

------

​	1, alert,   console, 不能在模板语法中运行;   因为在vue的环境下, this的指向不是window, 而是vue实例对象, 这一点与react一致

​	2, Vue的模板语法采用类似jsx的mustache语法糖, 所有使用规则和react一致, 只不过在html中使用是 {{ }} (两个大括号)包裹

​	3, 对于虚拟dom的操作和react一样, 是采用自己的事件进行控制

​	





- Vue 与react一样, 当数据发生变化, 视图也会跟着变化. 数据驱动视图渲染

- Vue 有俩个内容组成
  - 1, 指令
  - 2, 组件

- 指令

  - 1, vue中使用v-xxx来表示一个指令, 这个指令写在标签的属性中

- 4, 属性中不谢mustache语法, 内部中要写的. 属性中不写 {{ }}

- 5, 如果 new Vue(option) 如果没有el选项, 我们可以进行手动装载

  ` new Vue({ }).$mount('#app') `

- 

  ```
  <ul id="app">
  	<li v-for=" item in arr " >{{ item }}</li>
  </ul>
  
  new Vue({
      el:"#app",
      data:{
          arr: { a, b, c, d }
      }
      
      
  })
  ```

  

  ### 列表渲染

  ------

  

- `v-for  = ' (item, key, index) in data '`    // 数据,    键值,    索引号

  + `index` : 索引
  + `item`: data中的元素
  + `key`:  如果是对象,表示对象的key

- `v-for`如果有循环嵌套, 那么value可以写成一样的命名, 但是不建议

- `v-for` 可以循环遍历**数字**和**字符串** 

- `v-for` 就是一个函数 

  ​	

### 条件渲染

------

​	**俩者:**

+ `v-if`

  + 单路分支

  + 双路分支

    ```
    <p v-if=" f " > 
    		true
    </p>
    <p v-else>
    		false
    </p>
    ```

  + 多路分支

    ​	```javascript

    <div id = "app">
        <p v-if = ' f === 1 '>  
            1
        </p>
        <p v-else-if = " f === 2 ">  
            2
        </p>
        <p v-else-if = " f === 3 ">  
            3
        </p>
        <p v-else>  
            4
        </p>
    </div>

    ​	

    ```
    
    ```

+ `v-show`

  + 如果条件为假, v-show有较高的初始渲染开销
  + 如果频繁的进行切换, 则v-if的渲染成本较高

  

  **项目中建议**

  ​	如果需要非常频繁的切换, 则使用v-show会节省性能多一些

  

  

  **`v-if` 操作的是DOM存在与否. 如果 v-if 判断为`false`, 这个元素都不存在**

  **`v-show` 操作的是`DOM`的`display`属性**

  

```
 <div id="app">
 			<p v-if = " f " > if条件 </p>
 </div>
 
 new Vue({
     el:"#app",
     data:{
         f:true
     }
 })
 
 
```

### 事件

​		**事件对象的实际参数  ==>   $event**

#### 事件的高级
##### 1, 事件修饰符
			举例: 事件冒泡
			通过举例告诉大家, e.stopPropsagation()这个代码的复用性差
			所有vue这边有一个解决方案:  使用事件修饰符(modify)
				
				格式:
				v-on:onclick.stop = " handleClick "  // 阻止事件冒泡
				
				v-on :eventType.modify = " eventFnName "
				
				类型 :
					.stop   	:  阻止冒泡行为
					.prevent  	:  阻止浏览器默认行为
					.capture	:  阻止捕获行为
					.self		:  自身出发
					.once		:  只执行一次
					.passive    :  行为结束后触发


​				
##### 2, 按键修饰符  ( 键盘事件:  keyup, keydown, keypress,  ) 
​	        @keydup.enter  
​	        .enter
​	        .tab
​	        .delete (捕获"删除" 和 "退格" )
​	        .esc 
​	        .space
​	        .up
​	        .down
​	        .left
​	        .right
​	        .p
​	        .a
​	       ​	      ​	        
##### 3, 自定义按键修饰符
	    	1, 全局修改
	    		Vue.config.keyCodes.f1 = 112
	    		
	    		// Vue.config.keyCodes.自定义修饰符 = 键盘码


​	    	2, **自定义事件** 
​	    		`v-on:my-event = eventFnName`
​	    		`触发: this.$emit(my-event)`

​			1, 如何定义:

​				使用` new Vue() `得到的实例来定义

​					`new Vue({ }).$on( eventName, callback )`

​			2, 如何触发

​				`new Vue( {} ).$emit(eventName)` 



​		事件中留有一个知识点:

​				原生事件调用






```javascript
/*
    事件:             --- 源生js中的操作
    	1, 属性绑定
    	 function alertHello() {
        	alert("hello word")
       	 }
      	 app.addEventerListen('click', alertHello)
        
    	2, js操作
    		// 1, 获取数据
    			var data = "hello vue.js"
    		// 2, 获取DOM
    			var app = document.queryselector("app")
    		// 3, 渲染数据
    			app.innerHTML = "data"
    		// 4, 添加事件
           	 	app.onclick = function () {
           	 		app.style.background = 'red'
           		}
           		
           事件的组成部分:
           		1, DOM
           		2, on 添加事件的形式
           		3, 事件类型   click
           		4, 事件处理函数
           		
          Vue 使用了第一种事件添加的形式 -- ** v-on **
          	格式:
          		v-on: eventType = eventFn
            简写:
               	@eventType = eventFn
          事件处理函数写在配置项中的 methods中
          
          
          书写步骤:
          		先写方法, 再去绑定
          
          需求:  
          	我们有一个方法, 这个方法中有两个参数, 第一个参数自定义, 第二个是事件对象			
          	
          	问题: 第二个参数   事件对象 = undefined\
          	
          	原因:  当我们传入自定义参数后, 系统无法自动识别, 是不是事件对象
          	
          	解决:  传入事件对象的实际参数, $event
          
          
*/

<div id = "app">
    <h3>事件添加</h3>
	<button v-on:click = "changeMsg" > {{ msg }} </button>
	<button @click="changeMsg2("hello") "> {{ msg2 }} </button>
</div>



new Vue({
    el:"#app",
    data:{
        msg: "hello vue.js",
        msg2: ""
    },
    methods:{
        changeMsg(){
            this.msg = "这是一个测试的demo"
        }
        changeMsg2(str) {
    	this.msg2 = str
		}
    }
})



new Vue({
    
}).$mount('#app')   // 另外一种挂载实例的方法 -- 手动挂载

```





### 单向数据绑定和双向数据绑定

------

​		**单向数据绑定:**

​			1, 概念:

​				将数据和属性进行绑定, 也就是原生身上的属性的值就是数据

​			2, 格式

​				`v-bind:attr = data`

​					简写:  ` :attr = data `:

​						` :value = "msg" `

​		**双向数据绑定**

​				1, 概念:   视图   < === >  数据

​					当视图或者数据有一方发生了变化, 则另一边也会发生改变

​				2, 格式:

​					`v-model:attr = data`

​			( 应用,vue只有在**表单元素**才是**双向**绑定, 其他的数据都是**单向**数据流. )

​			( 与React的差别:

​		react推荐让我们使用受控组件进行数据获取, 但是. 在表单元素中, 我们通过

`value={ val => this.setState({ value: val }) }`也只能获取视图层的数据, 并不能直接修改. 只能通过`this.setState`来改变状态以修改视图层的数据



​			但是Vue中的 `v-model`方法, 属于双向数据绑定, 当视图层的数据发生改变, 数据也会随之改变, 我们无论是操控数据,还是操控视图,都可以直接控制另一方									

 )



### 类名绑定

​		通过操作数据 ==>  控制 ==> 类名 ==>  css样式



