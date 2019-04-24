## `redux`理解:

​		收集组件的状态并且统一管理,解决跨组件传值的困难性



 

### 安装

+ `npm install --save redux;`
+ `yarn add redux`





### `redux `工作流程图



​		![](C:\Users\25445\Desktop\Redux工作流程.png)



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
+ 





### 案例代码 - 例子见我的React-dome 库

​	