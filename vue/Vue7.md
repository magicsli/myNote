# 笔记七



## 路由

安装:

​	` yarn add vue-router -S ` 



创建router文件夹

 



引入路由

```javascript
import Vue from 'vue';
import vueRouter from 'vue-router';
Vue.use( vueRouter )
```







创建路由表

```javascript
const routes = [
    {
        path, // 当前路由的路径
        
        component, // 当前路由对应的组件
        
        children: [    // 子路由
       		{  }
		], 
        name,       // 命名路由, 避免使用多级路径写法 
    	
    	redirect    // 默认重定向
    }
]

```







使用配置

```javascript
const router = new VueRouter({
    // 路由表
    routes,   //必写的
    
    // 路由的使用模式
    mode:'history' ,
    
    // 路由模块
    modules: {
        
    }
})
```

注: // 路由的使用模式    mode 

`#/home   hash路由   `  传统的url hash路由  

​	- 如果你用hash路由,那么跳转就直接用a就好了

`/home    h5  history  API 和服务器配置`  , **需要后端支持**

​	- 用新路由, 就用router-link

`absreact -  支持所有javascript运行环境, 如 Node.js服务器端, 若果发现没有浏览器的api, 就会自动进入这个模式`





注册路由库

```javascript
import router from './xxx/router'

new Vue({
    router, 
    render: h => h(App)
})
```







**路由展示  `<router-view>  </router-view>`**



​	

### 二级路由

```javascript
const routes = [
    {
        path:'/home',
        component:Home,
        children:[
            {
                path:'about',   //注意:二级路由不要加 /
                component:About
            }
        ]
    }
]
```

- 注意: 写好配置后, 不要忘记在一级路由的组件中书写展示区域







#### 命名路由

```javascript
const routes = [
    {
        path:'/home',
        component:Home,
        children:[
            {
                path:'about',
                component:About,
                name:'about'
            }
        ]
    }
]
```
**用法**

```vue
<template>
	<div class='home-about'>
       <router-link :to:'{name:'about}'> about </router-link>
   
    </div>

</template>
```







### 动态路由传参 - 路由传参 - 路由接参





### 命名路由

​	给路由取个名字, 这样我们在使用的时候,简写路径

` <router-link :to='{name: 'about'}></router-link>'`

```javascript
const routes = [
    {
        path:'/home',
        component:Home,
        name:'about'
    }
]
```







### 命名视图

​	给出了一级视图以外的其他视图起名字, 这样可以区分不同级别的路由使用不同级别的视图

​	` <router-view name='socend'></router-view> `

​	

```javascript
const routes = [
    {
        path:'/home',
        component:Home
        childrenL[
       		 {
        		path:'food',
                components:{
               		second:Food
            	},
    			name:'food'
    		 }
        ]
    }
]
```









### 配置反向代理

​	**配置vue.config.js** 

`vue.config.js中默认直接使用http-proxy-middleware`

​	配置 `devServer.proxy`

```javascript
module.exports = {
    devServer: {
        proxy: {
            '/siku': {   // /siku是一个标记, 
                target: 'https://android.secoo.com',  // 目标源
                changOrigin: true,   // 修改源
                pathRewrite: {
                    '^/siku' : ''  // 请求时去掉标记
                }
            }
        }
    }
}
```

**stylus**

​	sass语法 + pug

声明变量 用`$` 符号             `$color = 'red'`

利用空格确定层级

```stylus
$color = 'red'
.food-box
    ul
        list-style none
        display flex
        justify-content space-around
        flex-wrap warp
        li
            padding 10px
    
    
```

### 路由传参

`<router-link  to="{name:'Home', params:{ value:122, keyword:123 } }"`	

router-link还有两个参数  `params`  和 `query`

params可以进行传参

query用来设置路径值

```html
<router-link :to = "{name:'list', params:{id:xxx}, query:{xxx:xxx } }"></router-link>
```

- 路由的接参

  - 我们发现凡是使用了路由的组件, 我们统称路由组件

  - 路由组件身上会有一个数据, $route 数据

    ```javascript
    id : this.$route.params.id
    query: this.$route.query.xx
    ```

    

#### 编程式导航

 - push 

   `this.$route.push('/category')`

   `this.$route.push({name:'home', query:'', params:'' })`

   push可以将我们的操作存放到浏览器的历史记录

   

 - replace

   用法和push一致, 不过不回保存在历史记录

+ back

  ​	返回

+ go





## 路由进阶  -- 导航守卫 ( 路由守卫 )

+ 1, 作用:    

  + 守卫路由
    + 进
      + 举例:  携带数据进
    + 出
      + 举例: 事情完成了才能出

+ 2, 导航守卫一共有三种形式

  + 全局导航守卫

    + **全局前置守卫**     `router.beforeEach(fn)`
      + `fn`中有三个参数 ( to, from, next )
        + to   前往
        + from   从哪里来
        + next     过

    

    + 全局解析守卫

      ​	在 2.5+ 你可以使用`router.beforeResolve`注册一个全局守卫,这回`router.beforEach`类似, 区别是在导航被确认之前,同时在所有组件内守卫和异步路由组件被解析之后, 解析守卫就被调用

      ​	**必须保证整个项目的守卫和异步路由组件解析完成**

    

    

    + 全局后置守卫; 这个钩子没有next存在
      + 可以做一些用户友好提示, 

    

  ​	

  

  + 路由独享守卫
    + 写在路由表中的守卫钩子

  ```javascript
  const routes = [
      {
          path:'/login',
          component:Mine,
          beforeEnter: (to, from, next) => {
              console.log('to', to)
          }
      }
  ]
  ```

  + 针对的是和当前路由相关的, 那么其他与之不相关的路由是无法监听的

  

  

  + 组件内守卫

    + **`beforeRouteEnter`**    进入组件前
      + 渲染该组件的对应路由被confirm前调用
      + **不能!!!!!** 获取组件实例 `this`
      + 因为当守卫执行前,组件实例还没有被创建
      + 我们想要将获得的数据给组件, 可惜我们这个钩子中获取不到组件的this
      + vue给了一个方案, `next()`中可以传递一个**函数**作为参数
      + 我们现在挂在组件身上的数据,是非响应式的,但是我们必须做成响应式
      + 解决:  `Vue.set() `  或者  `this.$set`

    ```javascript
    export default {
        beforeRouteEnter(to,from, next){
            axios.get('/siku/....', {
                params:{
                    v:2.0,
                    _:11564315845,
                    callback:'json1'
                }
            })
                .then( res => {
                console.log('res', res)
                
       //         next( vm => vm.category = "1212") // 这样是有问题的
                
    // next()            
                
            } )
            	.catch( err => console.log( error ) )
        },
        
    }
    ```

    

    

    

    + **`beforeRouteUpdate`**   组件更新前
      + 在当前路由改变但是该组件被复用是调用
      + 举例来说, 对于一个带有动态参数的数据`/food/:id`和`/foo/2`之间跳转的时候
      + 由于会渲染同样的foo组件, 因此组件实例

    

    

    

    

    + **`beforeRouteLeave`**   离开组件前

      同样有 to from  next 几个属性, 只有执行next才允许离开





+ 功能: 导航守卫可以监听路由变化情况
+ 名词:   

  + 前置:  要进入当前路由	-- 进入前
  + 后置:  要离开当前路由        -- 进入后
+ 关于next的使用
  + next() 等价于 next( true )
  + next(false) 表示不通过, 表示从当前路由跳转不到目标路由
  + `next( '/login' ) `跳转到指定的路由
    + 等价于 `next( {path:'/login'} )`
  + `next( fn )` 数据预载的时候用



+ 业务, 当我们进入到一个项目的首页时, 但是我们没有登录账号, 他主动跳转到登录页

```javascript

router.beforeEach( (to, from, next) => {
    const name = localStorage.gitItem('name');
    if(name && to.path === '/home'){
        next()
    }elst if (to.path === '/login') {
        next( );
    }else{
    	next( 'login' )
    }
    
})


```

注:  获取locaStorage中的name属性, 若用户登录了,则有这个属性, 判断用户是不是跳转到home, 如果是,则让他通过, 如果没有name, 或者不是前往home,则让他登录

 

+ 业务, 当进入mine页的时候要判断用户是否登录, 如果没有登录,跳转登录页

  ```javascript
  const routes = [
      {
          path:'/login',
          component:Mine,
          beforeEnter: (to, from, next) => {
             const name = localStorage.getItem('name');
              if(name && to.path === 'mine'){
                  next()
              }elst{
                  setTimeout(()=>{
                      alert('您没有登录, 500毫秒后跳转')
                       next('/login')
                  } ,500)
                 
              }
          }
      }
  ]
  ```

  

​	



