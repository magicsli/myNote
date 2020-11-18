# vue3.0试水笔记

## setup



+ 概念: 官方文档提出的这个组合性api想以替换以前的data方式以及生命周期. 我们能在setup设置一些和data同等级的响应式数据

  ```javascript
  export default {
      setup(props, context) {
          
          // 使用ref创建一个响应式数据
          const count = ref(0);
          
          // 使用reactive创建一个响应式数据
          const state = reactive({count: 0})
          
          /* 补充一点, 由于vue3.0使用的proxy作为数据代理, 所以我们在响应式数据的时候, 切记不能直接用解构复制, 这会破坏其响应式 */
          // 错误写法
          const { state } = ref({state:2});
          const { count } = props;
          
          /* 在3.0中如果需要获取响应式数据 */
          const state = ref( {state: 1} );
          console.log(state.value.state)
          
          /* 在3.0中如果需要获取props中的值 */
          const { count } = toRefs(props)
          
      }
  }
  ```

  

## 生命周期

vue3.0中部分的生命周期进行部分变化,且在setup中也可以进行使用:

<table><thead><tr><th>选项式 API</th> <th>Hook inside <code>setup</code></th></tr></thead> <tbody><tr><td><code>beforeCreate</code></td> <td>Not needed*</td></tr> <tr><td><code>created</code></td> <td>Not needed*</td></tr> <tr><td><code>beforeMount</code></td> <td><code>onBeforeMount</code></td></tr> <tr><td><code>mounted</code></td> <td><code>onMounted</code></td></tr> <tr><td><code>beforeUpdate</code></td> <td><code>onBeforeUpdate</code></td></tr> <tr><td><code>updated</code></td> <td><code>onUpdated</code></td></tr> <tr><td><code>beforeUnmount</code></td> <td><code>onBeforeUnmount</code></td></tr> <tr><td><code>unmounted</code></td> <td><code>onUnmounted</code></td></tr> <tr><td><code>errorCaptured</code></td> <td><code>onErrorCaptured</code></td></tr> <tr><td><code>renderTracked</code></td> <td><code>onRenderTracked</code></td></tr> <tr><td><code>renderTriggered</code></td> <td><code>onRenderTriggered</code></td></tr></tbody></table>



**总结**: 其实吧, 如果学过react hooks的都知道, 这个思想和hooks非常接近, 可以说是半个抄袭了, hook的核心.但是hooks去除了生命周期的概念, 但作为最常用的几个操作, 请求数据, 清除计时器. 都需要周期, 

```react
import { useState, useEffect } from 'react'

function Count(props) {    
    // 定义状态, 修改状态的方法
	const [count, setCount] = useState(0);
    
    // 副作用操作 - 依赖于count的副作用
    useEffect(() => {
        console.log(count);
    }, [count])
}	


```

