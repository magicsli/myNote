

## 基础操作

**微信路由API**

```javascript
wx.switchTab      // 切换tab栏(app.json中设置的tabBar)
wx.reLaunch       // 关闭所有页面, 重新打开指定的这个页面
wx.rediectTo	  // 在当前页面重定向到指定页面
wx.navigateTo	  // 前进
wx.navigateBack	  // 后退
```



### 交互

**简介**

```javascript
wx.showToast( {} ) 		// 显示消息提示框
wx.showModal( {} ) 		// 显示对话框
wx.showLoading( {} )	// 显示加载对话框
wx.showActionSheet( {} )	// 显示操作菜单
```



**事件** ( 触发器:   bind 不会阻止事件冒泡,    catch 会阻止事件冒泡 )

```javascript
touchstart	// 手指触摸动作开始
touchmove 	// 手指触摸后移动
touchcancel	// 手指触摸动作被打断 如来电提醒, 弹窗
touchend	// 手指触摸动作结束
tap			// 手指触摸后马上离开  ( 点击 )
longpress	// 手指触摸后, 超过350ms再离开, 如果指定了事件回调函数并触发了这个事件, tap事件将不再触发
transitionend	// 会在动画结束后触发
animationstart	// 会在动画开始时触发
animationiteration	// 会在动画一次迭代结束时触发
animationend	// 会在动画完成时触发

/** 
*  触发器:   bind 不会阻止事件冒泡,    catch 会阻止事件冒泡
* 用法: 	bindtap
* 或者:   bind:touchstart
**/
```







**消息提示框**

```javascript
wx.showToast( {} )  // 显示消息提示框 示例:
/*

	wx.showToast({
		title: "成功",        // 提示内容
		icon:"success",		 // 提示图标, success, loading, none(无图标)
		duration:2000, 		 // 停留时间
		image: '',			 // 自定义图标的本地路径 优先级高于icon
		mask: true,			 // 遮罩层
        success / fail / complate  日常三个回调函数
	})
	
*/
```



**对话框**

```javascript
wx.showModal( {} ) // 显示对话框, 示例:
/*

	wx.showModal({
		title: "你真的要删除吗?",     // 对话框标题
		content: "提示: 删除了就再也回不来了, 这可能会对您造成不可挽救的损失", // 提示内容
		cancelText: '我点错了', 	 // 取消按钮的文本
		cancelColor: "#a1b2c3",		// 取消按钮的文字颜色
		confirmText: '我确定要删除',	// 确认按钮的文本
		confirmColor: '#a33333', 	// 确认按钮的文字颜色
		常用回调函数: success / fail / complate 
	})

*/
```







**获取用户目前的经度 / 维度**

```javascript
wx.getLocation({
    type: 'wgs84',
    success: res => {
        const latitude = res.latitude // 维度
        const longitude = res.longitude // 经度
    }
}) 
```

  获取用户的地理位置并展示在地图上 （ 配合`<map>`标签使用）例:

```javascript
page({
    data: {
        latitude: null,
        longitude: null
    }
    
    onShow() {
        wx.getLocation({
            type: 'wgs84',
            success: res => {
                this.setData({latitude:res.latitude })  // 维度
                this.setData({longitude:res.longitude })  // 经度
            }
        }) 
    }
})



```

```html
<map longitude = "{{longitude}}" longitude = "{{longitude}}"> <</map>
```

-- 可以进行地图定位 -- 





**调用微信扫一扫功能:**

```javascript
wx.scanCode({
    success: res => {
        console.log(res)
    }
})
```



**`App`界面`API`:**

```javascript
// app.js
App({
  onLaunch (options) {
    // 小程序初始化时触发
  },
  onShow (options) {
    // 小程序显示时触发
  },
  onHide () {
    // 小程序隐藏 ( 进入后台模式 )
  },
  onError (msg) {
      
      // 出现错误时触发
    console.log(msg)
  },
  globalData: 'I am global data'
})
```









**页面`API`:**

```javascript
Page({
  data: {
    text: "This is page data."
  },
  onLoad: function(options) {
    // 当页面初始化时
  },
  onReady: function() {
    // 准备好页面后再做一些事情。
  },
  onShow: function() {
    // 当页面显示时，执行一些操作。
  },
  onHide: function() {
    // 当页面隐藏时做一些事情
  },
  onUnload: function() {
    // 当页面卸载时做一些事情
  },
  onPullDownRefresh: function() {
    // 下拉时
  },
  onReachBottom: function() {
    // 上拉时
  },
  onShareAppMessage: function () {
    // 当用户共享时返回自定义共享数据。
  },
  onPageScroll: function() {
    // 页面滚动式触发
  },
  onResize: function() {
    // 页面大小发生变化时触发
  },
  onTabItemTap(item) {
    console.log(item.index)
    console.log(item.pagePath)
    console.log(item.text)
      // 当用户点击tab栏时触发时间
      
  },
  // Event handler.
  viewTap: function() {
    this.setData({
      text: 'Set some data for updating view.'
    }, function() {
      // this is setData callback
    })
  },
  customData: {
    hi: 'MINA'
  }
})
```



**事件触发:**

 ```html
<view  data-temp="测试数据" bindtap="tapName"></view>
 ```

我们就可以通过设置的data-temp的props值来为bindtap传递自定义数据 :

```javascript
Page({
    tapName(e) {
        console.log(e)
    }
    /*
    {
      "type":"tap",
      "timeStamp":895,
      "target": {
        "id": "tapTest",
        "dataset":  {
          "temp":"测试数据"
        }
      },
      "currentTarget":  {
        "id": "tapTest",
        "dataset": {
          "hi":"WeChat"
        }
      },
      "detail": {
        "x":53,
        "y":14
      },
      "touches":[{
        "identifier":0,
        "pageX":53,
        "pageY":14,
        "clientX":53,
        "clientY":14
      }],
      "changedTouches":[{
        "identifier":0,
        "pageX":53,
        "pageY":14,
        "clientX":53,
        "clientY":14
      }]
    }
    */
    
})
```



**用户登录**

```javascript
wx.login({
    success: res => {
        // 如果用户已经登录了, 则返回一个错误对象
        /*
        	{
				code: "081VEs7o1D3gWp0oJI5o1gCB7o1VEs7C"
                errMsg: "login:ok"
                __proto__: Object
            }
        */
    }
})
```



**获取用户授权状态**

```javascript
wx.getSetting({
    success: res => {
        if(res.authSetting['scope.userInfo']){
            // 已经通过授权, 可以直接通过 getUserInfo 获取头像昵称
        }
    }
})
```



