### 自定义组件流程

+ 1, 定义一个组件

  + 一个单文件的Vue文件

+ 2, 注册组件

  ```javascript
  var Loading = {
      install () {
          
          Vue.component('Loading', Loading)
      }
   
  }
  export default 
  ```

  

+ 3, 使用组件

  ```javascript
  import Loading from './xxx/Loading/index.js'
  
  Vue.use( Loading )
  ```

  







```javascript
--------------------index.js ( 插件文件夹 ) ------------------
import Vue from 'vue';
import Loading from './app';

export default {
    install () {   // 必写的
    	Vue.component('Loading', Loading)
	}
}


// 若有多个组件
export const Loading = {
    install () {
        Vue.component('Loading', Loading)
    }
}


export const Banner = {
    install () {
        Vue.component('Banner', Banner)
    }
}
```





```vue
---------------------app.vue--------------------------------
<template>
	<div>
        Loading
    </div>
</template>

<script>
    export default {
        
    }

</script scoped>

<style >
	

</style>

```



```javascript
----------------------- main.js-----------------
    import Loading from "./until/loading" // (Index文件可以省略)

	Vue.use( Loading )  // 注册组件

	
```

**发布到npm**

​	`npm adduser`

​	`npm publish` 





















