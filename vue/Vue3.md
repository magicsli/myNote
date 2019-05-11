# 笔记三

## 1, vue深入响应式原理

​	数据模型 ==> vm中的data选项

​	状态管理 :

​			**什么叫做状态**?    ==> 我们使用一个数据去管理视图中的一个部分, 那么这条数据就叫做状态管理

​	响应式原理:

 		**当视图模型(VM) 的数据模型发生改变时, 视图(V) 就会进行更新**

+ 底层原理:  
  + 1, Vue通过watcher将data中的属性全部使用`Object.defineProperty`编程`getter`和 `setter`, 当属性值发生改变的时候, 就会触发; 然后`watcher`就会触发,,让视图进行重新渲染
  + 2, **数据必须放在`data`**选项中, 才能进行深入响应式
  + 3, 核心使用的是`ES5 `的方法 , 这个方法**不支持**`IE8`及其以下

​		        ===>  	**`Object.defineProperty`**          < === 

​	我们也可以通过`this.$set( vm, prop, value ) ` // 实例内

​	`Vue.set(vm.someObj, prop, value )`                // 实例外

​	`Vue.set`的底层源码 :

​		将一个对象合并到另一个对象   ==  `Object.assign(目标对象, 当前对象)`





​		`Object.defineProperty(obj, obj.attr, descriptor)`

​			参数:

​				obj   ==>    要在其上定义属性的对象

​				prop  ==>     要定义或修改的属性的名称

​				descriptor   ==>     将被定义或修改的属性描述符 ;  它是一个对象   					`configurable`: 决定了对象的Key是否可删除

​					`enumerable`:       决定了对象是否可遍历( 枚举 )

​					`writeable` :   决定了对象的key的value是否可修改

​						-- get 函数   --   设置当前对象的key的初始值

​						-- set 函数   --    修改当前对象的key值, 当key值发生变化吗set函数会自动调用



​	**响应式原理: **    -- 当value发送变化, 自动调用set函数, 进行重新赋值

```
	var obj = { 
		name : '你好'
	};
	
	
	Object.defineProperty( obj, 'name', {
        get(){
            return '我被初始化了';
        },
        set(value){        // value 就是修改后的对象的key的value值
        
            console.log( " set被调用 " );
            console.log( " value的值被修改为 " + value );

           document.querySelector("#app").innerHTML = value;
        }
        
        
	} )
	
	document.querySelector("#app").innerHTML = obj.name
```



### 总结:

+ 1, 什么是深入式响应式原理?    ---   必问 

  + 深入响应式原理是利用了数据劫持 (get 和 set) 和订阅发布 ( 事件触发 ) 的模式,当数据模型发生改变的时候,视图就会发生响应的更新. 那么深入响应式原理就是利用`ES5` 的`Object.defineProperty ` 的  **get 和 set** 来进行数据劫持

    



​			名词解释:

​				数据劫持:   `Object.defineProperty中的getter和setter, 然后在执行watcher`

​				订阅发布:   事件 ( 自定义事件 )

​					订阅: 事件的声明   `vm.$on     Vue.on`

​					发布: 事件的触发`vm.emit`

+ 2, 非响应式情况
  + 在`vm`模型的data外定义的属性, 就是非响应式属性, 非响应式属性,  属性值更新  == 视图不会更新. 
+ 3, 非响应式属性如何变成响应式属性, 
  +  思维:   将非响应式属性合并到响应式属性身上
  + 解决:    利用了`Vue`提供的 ` Vue.set / this.$set(vm.dataattr, prop, value)`

+ 4, `Vue.set`的底层原生是什么:?
  + `Object.assign( 目标对象,  对象1,  对象2,  对象三)`

## 2, `vue`双向数据绑定原理

### 原理:

+ 1, 为什么数据能直接在视图显示

  + `v-model默认绑定了DOM对象的value属性`, 当他初次绑定的时候, 就会触发`gettet,   watcher就会触发.对虚拟DOM进行修改,  触发`render函数`

+ 2,  为什么视图修改数据就会修改

  ​	当视图修改时, 意味着DOM的value属性改变了, 就会触发`Set`, `watcher监听机制就会执行,   watcher通知`Vue`进行虚拟DOM重构



## 3, axios fetch数据请求

## 4, watch监听

## 5, mixins

## 6, 虚拟DOM和diff算法

## 7, 列表渲染中的key的作用

## 8, 组件

