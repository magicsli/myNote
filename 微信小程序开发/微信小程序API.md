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

