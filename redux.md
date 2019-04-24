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

+ 标识要执行行为的对象

+ 包含两个方面的属性

  + type       标识属性,   值为字符串,   唯一,    必要属性
  + data       数据属性,    值类型任意    可选属性

+ 例子:

  ```
  const action = {
      type: "INCREMENT",
      number: 2
  }
  ```

  

+ Action Creator (创建 Action的函数):

  ```
  const increment = (number) => ({ type:"INCREMENT", number })
  ```

  





#### `reducer`













### 案例代码 - 例子见我的React-dome 库

​	