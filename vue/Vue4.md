# 笔记四

## 组件注册:

+ 1, `Vue.component(组件名称, 组件的配置 )`

+ 2, 在组件中使用components的配置项来表示

+ 3, 问题:

  + 1, 组件命名问题 

    +    Header   Footer ==>  header  footer
    +    组件有且只有一个根元素
    +    2, 大驼峰式写法

    ```javascript
        Vue.component( 'ZhangJun', { 
            template:'<h2></h2>'
        })
    ```

    

```html
                <div id="app">
                <!--这样写是报错的-->
                <ZhangJun> </ZhangJun>  


                <!-- 因为在html中, 标签名会被解析为小写-->
				<zhang-jun> </zhang-jun>

        </div>
```



## 组件通信

​	组件之间数据的交互传输被称为组件通信

组件通信, 无论效果如何, Vue都是单向数据流

### 父子通信

+ A, 绑定简单类型数据

  + 父组件中定义数据,通过单向数据绑定的形式, 将数据绑定在子组件的身上, 属性是自定义属性

  + 子组件通过配置项中的props接收数据, props可以是一个数组, 数组放的是自定义属性名称

  + 那么这个自定义属性可以像data中的数据一样在子组件的模板中使用

  + 父组件中数据一旦修改, 子组件数据就会修改, 所以这也是单向数据流

    

+ B:  绑定复杂数据类型           --  不推荐

  + 1, 父组件中的数据是一复杂数据类型, 那么父组件绑定数据的时候, 给子组件的是一个引用地址

  + 2, 子组件可以通过这个引用地址,修改这个数据

  + 3, 效果上像, 子组件个父组件通信了, 违背单向数据流




#### 子组件向父组件传值

+ C,  如果你想让子向父级传递数据, 可以通过回调函数的行为进行数据回调;**这点和React一致,原理很简单**

  

+ D, 通过自定义事件来进行通信:

  + 父组件中定义 数据 和 方法 ( 方法时用来操作数据 )
  + 在子组件身上绑定自定义事件
  + 子组件定义方法, 在这个方法中通过 this.$emit( eventType, 实际参数)来调用自定义事件的事件处理程序

  

  ####  父向子传值 例:

  ```html
  <div id="app">
      <son :money="money" >  </son>
  </div>
  ```

  ```javascript
  new Vue({
      el:'#app',
      data:{
          money:1000
      }
  });
  
  Vue.component('son', {
      template:'<div> {{ money }} </div>',
      props:['money']      // 这里不推荐使用数组, 虽然方便.但是缺乏验证
      
      /* 
      props:{
           money:{
              title: String,
            	likes: Number,
            	isPublished: Boolean,
           	commentIds: Array,
          	author: Object,
            	callback: Function,:
              }
      }
      ]
      */ 
  })
  ```





#### 自定义事件通信


  ```html
  <div id="app">
      <King></King>
  </div>
  
  <template id="king">
  	<div>
          <h3> I am KING </h3>
          <p>  国库中有 {{ gk }}钱  </p>
          <people @get='get' />
      </div>
  </template>
  
  <template id="people">
  	<div>
            <h3> I am people </h3>
          <button @click = "give"> 交钱 </button>
      </div>
  </template>
  
  
  ```

  ```javascript
  Vue.component('King', {
      template:'#king',
      data(){
          return:{
              get:0
          }
      },
      methods:{
          get(value){
              this.get += value
          }
      }
  })
  
  Vue.component( 'people', {
      template:"#people",
      data(){
          return {
              money: 2000
          }
      },
      methods:{
          give(){
              this.$emit('get', this.money / 2)
          }
      }
  })
  ```

  





### 兄弟通信

+ 使用ref来绑定组件, ( ref也可以绑定DOM元素 )	- ref链
  + 在父组件的模板中, 使用 `ref = 'name'`绑定在两个兄弟组件身上
  + 在任一个子组件中, 就可以通过`this,$parent1.​$refs.refName` 就可以获得另一个子组件了, 同时这个子组件身上的数据和方法也能得到了



+ 通过事件总线( BUS )

  - 利用 `var bus = new Vue()`中的$emit 自定义方法来进行数据

  - 首先, 在js中创建一个Bus对象(VM)

  ```javascript
  var bus = new Vue()
  ```

  - 在count组件中定义数据, 和修改数据的方法

  - 在count组件中通过created钩子, 进行bus事件的发布

```javascript
            created:{
                bus.$on('add', this.addCount)
            }
```

​		在Mybutton组件的方法中通过bus进行事件的订阅

```javascript
increment(){
    bus.$emit('add')
}
```





## 组件生命周期

+ **组件的几个阶段**:
  - 初始化阶段
  - 运行中阶段
  - 销毁阶段



### 初始化

 - 分为两个大阶段, 每一个大阶段包含两个生命周期钩子函数

    - 1,  `beforeCreate`	 	--  准备创建组件

       - 表示组件创建前的准备工作, 为事件的发布订阅 和 生命周期的开始做初始化    --  **没有生命实际用途**

      /*  组件未创建, 所以没有this, 数据拿不到, DOM也拿不到 */

   

   

    - 2,  `created`                            --  组件初始化完成    

       - 表示组件创建结束, 

       - 这个钩子函数中, **数据拿到了, 但是DOM没有拿到**    

       - 这个钩子在项目中:

          - **数据请求, 然后可以进行一次默认数据的修改**

         

         

    - 3,  `beforeMounte`                     --    准备挂载

       - 表示组件装载前的准备工作
          - 判断`el`选项有没有, 判断`template`选项有没有, 如果没有,则需要手动装载
          - 如果有, 那么通过`render`函数进行模板的渲染( 没有做, 处于虚拟dom阶段)
          - 这个钩子函数中, 
             - 数据拿到了, 真实dom没有拿到
             - 这个钩子函数在项目中
                - 数据请求, 它也可以进行一次数据修改

   

   

    - 4,  `mounted`                            --    挂载完成
       - 组件装载完成,就是我们可以在视图中看到了
       - 这个钩子函数中, 数据拿到了, 真实DOM也拿到了
       - 这个钩子函数在项目中
          - DOM操作就可以进行了, 第三方库的实例化
          - 如果进行数据修改,则会重新渲染



 - 总结:  数据请求越提前越好, created常用于数据的请求和数据的修改, 第三方库的实例化常在mounted中进行书写



### 运行 / 更新



### 组件卸载阶段











### 多组件状态共享

+ 使用Vue-Router
+ 使用状态管理工具



