# 笔记二

## class  &&  style

### class

#### 	1, 为什么要用绑定类名

+ 数据驱动视图 ==>  驱动  ==> 视图     数据 -- 控制 --> 类名

  #### 2, **类名** 要和 **数据** 绑定     绑定 ==  使用 ==>  v-bind

​		`  `

##### 	// **注意** :    这里`size`不是实例对象中的数据,而是单纯的类名字符串;



#### 	3, 类名的绑定方式

+ A: 对象的形式

  `:class = "{ 'size' : classFlag }"`  // 如果`classFlag`是`true`则添加了一个size的类名

+ B: 数组的形式

  ​	` :class =" ['size', 'bg' ] " `

  

  

### style

#### 为什么要绑定样式

#### 	样式有几种使用形式:

+ 1, style 双标签嵌入样式

+ 2, 行内样式
+ 3, 外部引用
+ 4, `@import("./css/ ... ")`已被废弃, 只有只有预编译CSS的工具才会使用
+ 数据 == 控制 == 样式 ==> 功能  效果



+ 样式 -- 数据  绑定使用 ==>   `v-bind`

   

   `

  #### 样式的绑定形式:

  + A: 对象形式

    ​	` :style = "{ width:'50px', height:'60px' }"`

    ​	`:style = " style "` // 将数据放在`data`中

  + B: 数组形式

    ​	`:style = "[{width:'50px', height:'50px'}, style]"`





### 计算属性

+ 1, 为什么要有计算属性?

  + 1, 直接模板语法中写逻辑,   // HTML结构不纯粹,  写起来不舒服
  + 2, 方法运行,   但是语义性不高

+ 2, 计算属性是什么?

  + 计算属性时 `new Vue(options)`  options中的一个配置项, 用computed表示,他的值是一个对象
  + 计算属性的值中存放的是方法

  ```
  nwe Vue({
      el:"#app",
      
      // 数据
      data:{
          msg:'demo';
      },
      // 事件
      methods:{
          reverseHandler(){
              return this.msg.split('').reverse.join('')
          }
      },
      // 计算
      computed:{
          reverseMsg(){
               return this.msg.split('').reverse.join('') 
          }
      }
  })
  ```

  

// **结论**  :     当这个实例使用的时,会自动调用实例上挂载的`computed`方法. 类似于 我们react中的 `render`, 会自动调用



**computed 和 methods的区别**

+ 同:  都是函数, 都可以书写逻辑
+ 异:  `methods`中的方法依赖于事件或者是方法调用,  
  - 但是`computed`的方法名可以直接当作变量使用, 类似于直接在data中定义的数据

4,  在项目中使用计算属性的条件:

+ 有逻辑
+ 使用类似变量