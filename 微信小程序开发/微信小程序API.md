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



