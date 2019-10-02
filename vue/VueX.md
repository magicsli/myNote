# VueX

+ 什么是状态？

  - 用一条数据去管理一个视图或是视图中的一部分，那么我们就将这个数据称之为**状态**
+ 什么是状态管理？
  - 用一条数据去管理一个视图或是视图中的一部分，那么我们就将这个数据称之为**状态**，这种管理的形式我们称之为 **状态管理**
+ vuex是做什么的？（概念）
  - vuex是一个集中式的存储仓库【状态】，类似于 本地存储、数据库，vuex是vue的状态管理工具，它的功能主要是实现多组件间的状态【数据】共享
+ vuex的组成部分( 前三个是必答的，后两个可以不答 )
  - **state 状态**
  - **actions 动作（业务交互）**
  - **mutations 修改state**
  - getters 获取数据的
  - store  vuex核心管理者
+ 应用场景
  1. 相对比较大型的应用（状态较多）
+ 判断你的项目是不是应该使用vuex
  1. 当你觉得你的项目不需要vuex的时候，那么就不用
  2. 你觉得需要的时候，就直接使用 



7. 思维流程:
        store.js
   this.$store.commit('increment')    -> mutations
   this.$store.dispatch('jia')        -> actions            
     mapActions() ->actions                                mapGetters()->getters

```

```

 (view）component - dispatch >  action   ->  mutation ->    state  <- getter    <-    component
          发送请求      处理            修改状态         
                        业务逻辑        修改state                读取state
                        异步

8. vuex的使用方案有哪些？（state修改前，state修改后）

   1. 前标准，后标准           √
   2. 前标准，后非标准         √
   3. 前非标准，后标准         √
   4. 前非标准，后非标准       √

9. 问题

   1. 数据的获取写的太长了，冗余
   2. 视图和vuex的交互代码太长了，冗余

   - 解决： Vuex提供了4个辅助工具： mapState **mapGetters  mapActions mapMutaions**
         - mapState 我们可能不常用  

   - mapGetters([gettersFnName]) 使用   {{ gettersFnName }}

     ```javascript
        new Vue({
          //computed: mapGetters(['getCount']), // 这么写我们的当前组件的自定义计算属性就没有地方放了
          computed: {
            ...mapGetters(['getCount])
          }
        })
     ```

- mapActions([actionsFnName])  标准

  ```javascript
    new Vue({
      methods: {
        ...mapActions([actionsFnName])
      }
    })
  ```

- mapMutations([mutationsFnName])  非标准

  ```html
      <button @click = "mutationsFnName()"></button>
  ```

  ```javascript
    new Vue({
      methods: {
        ...mapMutations([mutationsFnName])
      }
    })
  ```

- 以上讲的都是用户交互，没有写数据交互

- **vuex 的数据交互**

- 注意： 

  - **vuex的数据交互写在actions里面**

- actions.js

```javascript
  const actions = {
      getDataInfo ( { commit } ) {
        fetch('/data.json')
          .then( res => res.json() )
          .then( data => {
            //获取到数据之后进行动作的创建和发送
            let action = {
              type: 'GETDATAINFO',
              payload: data
            }
            commit( action )

          })
          .catch( error => console.log( error ))
      }
  }

  export default actions
```

### vuex 中的 modules

- store目录中放的是目录

  ```javascript
  <!-- 目录结构 -->
    store
      index.js
      home
        state.js
        actions.js
        mutations.js
        getters.js
        type.js
        index.js
      shopcar
          state.js
          actions.js
          mutations.js
          getters.js
          type.js
          index.js
      list
        state.js
        actions.js
        mutations.js
        getters.js
        type.js
        index.js
      user
        state.js
        actions.js
        mutations.js
        getters.js
        type.js
        index.js
  // home  下的 index.js 
      import state from './state'
      import actions from './actions'
      import mutations from './mutations'
      import getters from './getters'
      const homeModule = {
        state,
        actions,
        mutations,
        getters
      }
      export default homeModule
  // store 下的  index.js 
    const store = new Vuex.Store({
      modules: {
        //key: value   // key就是目录名称， value就是目录下的index.js导出的模块
        home: homeModule
      }
    })
    export default store
  ```

- 作为5.1作业