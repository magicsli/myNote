#  笔记三

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

​				descriptor   ==>     将被定义或修改的属性描述符 ;  它是一个对象 :

  				      `configurable`: 决定了对象的Key是否可删除

​					`enumerable`:       决定了对象是否可遍历( 枚举 )

​					`writeable` :   决定了对象的key的value是否可修改

​					-- get 函数   --   设置当前对象的key的初始值

​					-- set 函数   --    修改当前对象的key值, 当key值发生变化吗set函数会自动调用



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



#### 非响应情况

​	1, 数组下标

```html
<div id = "app">
    <button @click = "change" > 点击 </button>
    <ul>
        <li v-for = '(item, index) in list' :key = 'index'>
        	<p>
                {{ item }}
            </p>
        </li>
    </ul>
</div>
```

```javascript
new Vue({
    el:'#app',
    data:{
        list:['a','b','c','d']
    },
    methods:{
        change () {
            this.$set(this.list, '0', 'junge')
        }
    }
})
```

- 解决方案 :   使用`Vue.set  ||    this.$set`





删除一个数组时, 可以使用arr.length = 0, 但是vue不会响应

解决方案: 使用splice( new Length )

当我们 





## 2, `vue`双向数据绑定原理

### 原理:

+ 1, 为什么数据能直接在视图显示

  + `v-model默认绑定了DOM对象的value属性`, 当他初次绑定的时候, 就会触发`gettet,   watcher就会触发.对虚拟DOM进行修改,  触发`render函数`

+ 2,  为什么视图修改数据就会修改

  ​	当视图修改时, 意味着DOM的value属性改变了, 就会触发`Set`, `watcher监听机制就会执行,   watcher通知`Vue`进行虚拟DOM重构进而触发render进行渲染  



## 3, axios fetch数据请求

​	Vue没有对AJAX进行封装, 所以我们需要使用第三方库发送请求:

​		axios fetch 两者都是基于**promise** 

-- 原生提供了两种数据请求方式,   1, **ajax**   2, **fetch**

axios:

​	

#### Axios的get请求        数据对象  ==>  params

//  发送get请求

```
1, ---------------------------------------------------------
axios.get('https://www.magicsli.com', {
    method:'get',
    params:{
        a:1,
        b:2
    }
}).then( res => {
 	console.log(res)
} ).catch( err => {
    if(err){
        console.log(err)
    }
} )

2, ----------------------------------------------------------
axios.post({
	url: 'https://www.magicsli.com',
	method:'get',
	params:{
        a:1,
        b:2
	}
}).then( res => {

    console.log(res)
    
} ).catch( err => {

    if(err){
        console.log(err)
    }
    
} )

```
#### Axios的post请求方法       数据对象  ==>  data

```
// 发送post请求:   !!! 会报错

1,    会报错, 这样传参会出现前端跨域问题. ( 其实请求是成功的 )  注意!!!!  注意!!
	 axios.post({
         url:'https://www.magicsli.com',
         method:'post',
         data:{
             a:1,
             b:2
         }
	 }).then( res => {
	 
         console.log(res)
         
	 } ).catch( err => {
	 
         if(err){
             console.log(err)
         }
         
	 } )


```

#####  Axios总结

+ **get**
  + 无参数:    `axios.get(url).then( (res)=>{} ).catch( (err)=>{} )`
  + 有参数:      

`	`

```
				axios({
                    url:'https://www.magicsli.com',
                    method:'get'	// 默认就是get, 可以省略
                    params:{
                       key : value
                    }
				})
```

+ **post**

  ​	**注意:    Axios的请求时有坑的,  如果我们直接使用官方文档, 会有未设置请求的跨域报错问题;  解决办法**:

  1,  **统一设置请求头** :

  `axios.defaults.headers.post['Content-Type']=application/x-www-form-unrlencoded`

  

  2, 使用 **` new URLSearchParams`**实例化一个params对象

  

  3, 使用params对象的**apend**方法添加数据

  ```javascript
  
  
  let params = new URLSearchParams();
  
  params.apend( a, 3 );
  
  params.apend( b, 4 );
  
  axios({
      url:'https://www.magicsli.com',
      method:'post',,
      headers:{
          'Content-Type':'application/x-www-form-urlencode'
      }
      data: params
  })
  
  
  
  ```


####  fetch:             

​		**注意**:  fetch的返回是一个`promise`对象, 我们可以通过**.`then`**的方式来书写.  我们至少要写**两个**`.then` 

  ####   get请求

​	**fetch的get请求传参需要直接在URL上设置, 我们可以使用Node.js提供的URL或者是querystring模块来讲对象转为string**

​	例:

​		   	

```javascript
fetch('https://www.magicsli.com?a=123&b=456')
		// 格式化数据
.then( res =>  res.text() )   //或者 res.json()  和res.blob()
		//输出
.then( data => console.log(data) )
.catch( err => err && console.log(err) )
```



#### post 请求

在post请求项中,有一些配置项:  

```javascript
fetch( url, {
    
    body: JSON.stringify(data),   // 请求携带的参数       
    
    cache: 'no-cache', // 请求缓存, 当开启时,发送同样的请求会从缓存获取, 就不会再像服务器发送
    credentials:  'same-origin', // 跨源凭证
    headers:{
    'user-agent' : 'Mozilla/4.0 MDN Example',  // 内核
    'content-type' : 'application/json'      // 内容格式
},
    method: "POST", // 请求格式
    mode:'cors' ,   // 表示跨域的形式为 cors
    redirect: 'follow',  // 重定向
    
    
} )
```



**注意!!!     我们在发送post请求时, 如果直接使用 {a:1, b:2 }这类的方法会报错, 且也不能像官网一样使用JSON.stringify(). 这样依然会报错**

**解决方案**: 

+ `new URLSearchParams( ['a', 1], ['b', 2] ).toString()`  来将data进行处理

+ 设置请求头   `"Content-Type" : "application/x-www-form-urlencode"`



### 切记, Axios 和 fetch 的 post方法都是有坑的, 

#### 解决方案:

+ 设置请求头
+ 通过 `new URLSearchParams()` ;来进行数据传参



## 4, watch监听

+ 1, 作用:	

  ​	用来监听数据的变换, 当数据模型( data选项,  m )发送改变时, watch就会触发

+ 2, 使用

  

#### 业务:

+ **methods:事件**

+ computed:
  + 1, 有逻辑
  + 2, 像变量一样使用  , 这个时候选computed
+ watch: 
  + 1, 有异步操作
  + 2, 开销较大









```javascript
1, key的value是一个函数

new Vue({
    
	watch:{
        
		key() { },
	}
})


2, key的value值是一个对象

new Vue({
    
    watch:{
        
        key:{
            deep:true / fasle,  // 深入监听
            handler(value, oldValue){
                console.log("key发生了变化")
            } // 监听的处理函数
        }
    }
})

watch中的key指的就是data选项中的key



new Vue({
    ek:"#app",
    data:{
        msg:'1233456'
    },
    watch:{
        msg(value, oldValue){
            console.log("msg数据发生了改变")
        }
    }
})


```



## 5, mixins

​	{ 组件即实例, 实例及组件 }

​	**概念:** mixins:   混合, 将根实例或是组件中的配置项, 抽离出来, 单独管理

#### 类型:

 ##### 	局部混入

```javascript
			var mixin = {
            	methods: {
                    sum(){
                        alert(10 * 10)
                    }
                }
            }
            
            new Vue({
                el:"#app",
                data: {},
                watch: {},
                mixins: [mixin],
           // 即使mixin里有了methods,  我们依然可以设置methods,  当发生冲突, 以Vue实例中的为准     
               	methods: {}
                computed: {}
            })
            
            
```

##### 	全局混入

​		注意:    由于全局混入会影响所有的组件, **不推荐**使用

​	









## 6, 列表渲染中的key的作用

​	**给虚拟DOM添加标记, 保证组件 / 实例 的唯一性;**

​	这点和我们的React中的`key`作用一致

​	如果没有可用 ,会产生问题:

​		VDOM是惰性的, 他有一个原则叫做就地复用

注意: 优先使用数据中能够识别的, 比如 :  id

   



## 7, 组件

​	**组件使用前必须注册**

​	**注意!    data除了在根实例的情况下,其他情况都是函数:**

+ 1, 函数有独立作用域,
+ 2, 函数有return返回值

组件的data选项必须有返回值

### 组件的注册方式:

+ 全局注册



```javascript
const Hello = Vue.extend({
    template:' <h2></h2>',
    data(){
        return {
            msg:'你好'
        }
    }
    
})

// 注册:    Vue.component(组件名, 组件的构造函数)

Vue.component('Hello', Hello)


简写:  Vue.component('Hello', {
    template: "<div>456666</div>",
     
}


```

+ 局部注册

​	// 只能在定义的这个组件环境内使用

```javascript
new VUe({
    el:"#app",
    component:{
        "Hello" : Hello
    }
})
```





### [组件名大小写](https://cn.vuejs.org/v2/guide/components-registration.html#%E7%BB%84%E4%BB%B6%E5%90%8D%E5%A4%A7%E5%B0%8F%E5%86%99)



定义组件名的方式有两种：



#### 使用 kebab-case

```vue
Vue.component('my-component-name', { /* ... */ })
```

当使用 kebab-case (短横线分隔命名) 定义一个组件时，你也必须在引用这个自定义元素时使用 kebab-case，例如 `<my-component-name>`。



#### 使用 PascalCase

```vue
Vue.component('MyComponentName', { /* ... */ })
```

当使用 PascalCase (首字母大写命名) 定义一个组件时，你在引用这个自定义元素时两种命名法都可以使用。也就是说 `<my-component-name>` 和 `<MyComponentName>` 都是可接受的。注意，尽管如此，直接在 DOM (即非字符串的模板) 中使用时只有 kebab-case 是有效的。





**所以,   ( 在dom中使用组件!!!!!! )  vue推荐使用  `red-block` 这类组件名**



**如果在JSX语法糖下, 也可以使用与react一致的组件命名**