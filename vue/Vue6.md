# 笔记六



### 动态组件 

- 动态组件就是component组件
- 组件身上可以绑定一个**is**属性, 用来表示一某一个组件



**:is相当于`switch`,选择符合条件的子组件进行渲染**

我们`html`中有一些标签是规定它的直接子元素, 比如 ul li ol li selector option table 这类型标签

不能直接用常规的组件使用方式, 必须对应直接子元素上绑定 is属性

```html
<div>
    <table>
        <tr>
        	<td>aa</td>
            <td>bb</td>
            <td>cc</td>
        </tr>
        <tr is='my-table'> </tr>
    </table>
</div>
```







### keep-alive组件

​	- 将组件的内容存在浏览器缓存中, 当我们需要重复渲染时, 就从浏览器缓存中去调用,这样可以减少性能消耗

```html
<keep-alive>
	<component :is:'A'></component>
</keep-alive>
```





### 异步组件

异步组件也是一个函数, 只不过这个函数使用promise, 函数有一个返回值

使用函数, 通过promise的异步返回组件

 

```javascript
const asyncCom = {
    createAsyncCom ({
    selector,
    asyncComName, 
    methods,
    data, 
    watch, 
    props, 
    filter,
    directives,
    components
    }) {
        var result = new Promise( (res, rej) => {
            res({
                    selector,
                    asyncComName, 
                    methods,
                    data, 
                    watch, 
                    props, 
                    filter,
                    directives,
                    components
                    })
        } )
        Vue.component( asyncComName, async () => {
            const tql = await result.then(res => res);
            return tql
        } )
    }
}

export default {
    createAsyncCom : asyncCom.createAsyncCom 
}

```





### 不常用指令``

+ `v-html`         类似于 `innerHTML`
+ `v-text`         类似于 `innetText`
+ `v-pre`           不解析模板 , 原样输出
+ `v-cloak`        解决 {{ }} 语法的原样输出的问题
+ `v-once`           只渲染一次 ,之后就保持第一次渲染完成之后的状态    