---

---

## `redux`理解:

​		收集组件的状态并且统一管理,解决跨组件传值的困难性



 

### 安装

+ `npm install --save redux;`
+ `yarn add redux`





### `redux `工作流程图



![Redux工作流程](./Redux工作流程.png)

+ `Action Creators` 创建一个 `action `对象 
+ store` 状态存储管理库
+ `action `对象:
  + 1,   `type`  --  类型
  + 2, `data`   --  数据
+ `store` 将旧状态和 `action` 传给` Reducers`
+ `Reducers `将 传过来的旧状态和 actions 对象进行处理, 并返回给Store一个新的状态
+ Store 更新状态并将其返回给组件对象



### 概念



#### `Store`对象

##### 	作用

​		`redux`库最核心的管理对象

##### 	内部的`API`

+ `state`   状态

+  reducer   根据老的状态,更新一个新的状态的函数

  

  ##### 核心方法

  + `getState()`		-- 更新状态
  + `dispatch(action)`    -- 分发事件
  + subscribe(listener)         -- 订阅监听

  

  ##### 编码

  + `store.getState()`
  + `store.dispatch({type:"INCREMENT", number})`
  + `store.subscribe(render)`

  

​		



#### 核心概念

#### `action`

+ ***标识要执行行为的对象***

+ ***包含两个方面的属性***

  + type       标识属性,   值为字符串,   唯一,    必要属性
  + data       数据属性,    值类型任意    可选属性

+ ***例子***:

  ```
  const action = {
      type: "INCREMENT",
      number: 2
  }
  ```

  

+ **`Action Creator `(创建 Action的工厂函数):**

  ```
  const increment = (number) => ({ type:"INCREMENT", number })
  ```

  





#### `reducer`

+ ***根据老的`state`和`action`,产生新的`state`的纯函数***

+ *** 样例 ***

   

  ```
  export default function counter(state = 0, action){
      switch( action.type){
          case "INCREMENT":
          	return state + action.data
          case "DECREMENT":
          	return state - action.data
          default:
          	return state
      }
  }
  ```

  

+ 注意:
  + 返回一个新的状态
  + 不要去修改原来的状态   -- 注意注意 :  我们是通过俩个新旧的虚拟`dom`树对比来更新数据,如果更改了老的状态就会出现对比错误



#### `store`

+ 将state, action与reducer联系在一起的对象

+ 如何得到此对象?

  ```
  import {createStore} from 'redux'
  import reducer from "./reducers"
  const store = createStore(reducer)
  ```

+ 此对象的功能:

  + `getState()` 得到state 
  + `dispatch(action)`: 分发action, 触发`reducer`调用, 产生新的`state`
  + `subscribe(listen)`:注册监听, 当产生了新的`state`时, 自动调用





***提示代码***:

预备:

​	创建一个reducer 函数



```
// 1, 生成store对象
	const store = createStore( reducer ) // 内部会第一次调用reducer函数得到初始state
	
// 2, 将 store 对象传给 app 组件
	< App store={store }  />

// 3, 我们在组件中调用store的方法更新状态
	this.props.store.dispatch( {type: xxx, data : number} )


// 完善以上代码 我们不要自己来定义action,  封装一个函数用于创建action对象;我们只需要调用这个函数就可以了
// 使用 action create
 
		+ export const add = (number) => ({ type:"xxx", data:number })

// 设置监听消息 store.subscribe(render)
// 当状态改变时,自动调用里面的回调函数 render
```

​	

### `react-redux`

+ 一个`react`的插件库

+ 专门用来简化`react`应用中使用`redux`

  

### 示例代码:

```
	// 我们使用的react-redux 中提供了Provider组件
	拥有了provider组件,我们不需要添加监听事件,只需要将渲染的组件放在其中例:
			render( <Provider>
						<App />
					</Provider>, document.getElementbyId("root")  	)
					
   	//  将我们需要的函数通过props值返回给组件,通过连接函数(写法比较乖)
   	 取消组件的默认导出
   	export default connect(
   		state => ({ count:state }),  // 要设置什么状态值  
   		{increment, decrment}  // 要传什么参数
   	)(App)  // 包装谁
   	
   	对组件进行包装

```



​	

### React-Redux思想:



### React-Redux将所有组件分为两大类



#### 1,  UI组件

+ 只负责`UI`的呈现, 不带有任何业务逻辑
+ 通过props接收数据,(一般数据和函数)
+ 不使用任何`Redux`的`API `
+ 一般保存在components文件夹下



#### 2, 容器组件

+ 负责管理数据和业务逻辑, 不负责UI的呈现
+ 使用`Redux` 的`API`
+ 一般保存在`container` 文件夹下

### React-Redux组件



#### Provider

​	让所有组件都可以得到state数据

​	

```
	<Provider  store={ store} >   // 委托Provider进行管理
			<App />
		</Provider>

```

#### connect()

​	用于包装UI组件生成容器组件

```
import { connect } from 'react-redux'  // 对组件进行包装
	connect( 
    	mapStateToprops,
    	mapDispatchToprops
    )( Counter )
```



#### mapStateToprops()

​	将外部的数据(即state对象)转化为UI组件的标签属性

```
const mapStateToprops = function (state) {
    return {
        value: state
    }
}
```

### redux异步编程

***`redux`默认不支持异步处理的***

***应用中又需要进行异步任务(`ajax`, 计时器)***



####通过插件进行redux进行异步编程

​	

​	***`npm install --save redux-thunk`***



调用`redux`的中间件方法:

​	`import { createStore,  applyMiddleware } form 'redux'`

​	`import thunk from "redux-thunk"`





`const store = createStore(`

​	`counter,`

​	`applyMiddleware(thunk)`  // 应用上异步中间件

`)`

 

在action中返回一个函数:

​	`export const incrmentAsync = (number) => () => {`

​		`return dispath =>{`

​			1秒之后才去分发action

​		`setTimeout( dispath(increment( number) ),1000)`

​	`}`

​	`}`



### `redux`调试工具包    `redux-devtools-extension`

+ 下载谷歌浏览器插件***  `redux-devtools*`**

+ 下载工具依赖包:

  + `npm install --save-dev redux-devtools-extension`

+ 编码:

  ```
  import { composeWithDevTools } from 'redux-devtools-extension'
  
  const store = createStore(
  	counter,
  	composeWithDevTools( applyMiddleware(thunk) ) // 再包一层
  )
  ```

  

​	

####使用`combineReducers`将我们的的`reducer`进行合并, 统一管理

```
export  default combineReducers({
	counters,    // 指定reducer对应的属性
	comments	 // 将定义的reducer管理函数放到这里进行整合管理
})

// redux向外暴露的state是一个什么结构?

	\*** 对象 ***/
	
	{ counter:2, comments:[] }

注解:将所有reducer函数的的值都获取了过来.

```

### 学习小结:

+ `redux`是一个进行状态管理的库,

![Redux工作流程](![Redux工作流程](./Redux工作流程.png))

+ redux中最核心的是store管理对象

+ 常用代码块:

  ```
  // store 模块 
  import {creatrStore, applyMiddleware} from "redux"
  import {reducer} from "./reducers/reducer"
  import thunk from "redux-thunk"
  const store = createSotre( reducer,
  	composeWithDevTools( applyMiddleware(thunk) )
  )
  
  
  // 
  ```

  