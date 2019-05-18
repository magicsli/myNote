## Vue脚手架

安装

`npm install @vue/cli -g`     cli3的版本

`npm install vue-cli -g`       cli2的版本



我们一台电脑只能使用一个版本的vue脚手架, 如果需要,我们就需要使用一个调节工具

` npm install @vue/cli-init -g `



注意, 安装优先级   npm < cnpm < yarn



安装 cli3 

​	`vue create  cli3`

安装cli2

​	` vue init webpack cli2 `

` vue init webpack-simble cli2 `   cli2的简易版本













## Vue-Cli3

- vue的文件 ==> 单文件组件

  - 单文件组件有三部分组成
    - template模板 ( 必写 )
    - script
    - style
      - `scoped` 解决css命名冲突, 给css样式独立作用域, 防止命名冲突

  ```javascript
  <template>
  		<div>
      		{{ msg }} 
      	</div>    
  </template>
  
  <script>
  		
              export default {
  data () {
      return {
          msg: "hello word"
      } 
  }
  } 
              
  </script>
  
  ```

  







