Hook 可以在不编写class的情况下使用state以及其他特性
	
起因: 
	在组件之间复用状态逻辑很难,
		- hook可以在无需修改组件结构的情况下复用状态逻辑
	复用组件难以理解, 为了产品需求, 我们的组件所使用环境会不断变化, 组件也会不断更新, 最后为了兼容需求, 往往会有许多臃余的功能代码叠在一起
		- hook将组件中相互管理的部分拆分成更小的函数
	

以下是官方介绍:

	那么，什么是 Hook?

Hook 是一些可以让你在函数组件里“钩入” React state 及生命周期等特性的函数。Hook 不能在 class 组件中使用 —— 这使得你不使用 class 也能使用 React。（我们不推荐把你已有的组件全部重写，但是你可以在新组件里开始使用 Hook。）











demo:

```react
import React, { useState } from 'react';

function Example() {
    const [count, setCount] = useState(0);
    
    return (
    	<div>
        	<p>倒计时{count}秒</p>
            <button onClick={ ()=>setCount(count + 1) }>点击</button>
        </div>
    )
}
```







`useState` 用户状态, 用于定义状态以及定义修改状态的函数

`useEffect`  作用, 用于定义此hook的生命周期的副作用操作函数