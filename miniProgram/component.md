### 一、逻辑层

<!-- tabs:start -->

### **绑定**

```html
<!-- 数据绑定 -->
<view> Hello {{name}}! </view>
<!-- 事件绑定 -->
<button bindtap="changeName"> Click me! </button>
```

```javascript
var helloData = { name: 'Weixin' }

Page({
  data: helloData,
  changeName: function(e) {
      //修改数据
    this.setData({ name: 'MINA' })
  }})
```

### **小程序生命周期**

- [官网](https://developers.weixin.qq.com/miniprogram/dev/reference/api/App.html)

```javascript
// app.js
App({
    //小程序初始化
  onLaunch (options) {},
    //监听小程序启动或切前台
  onShow (options) {},
    //监听小程序切后台
  onHide () {},
    //错误监听函数。
  onError (msg) {console.log(msg)},
    //其他 - 未处理的Promise拒绝事件监听函数  - 监听系统主题变化等 查看官网
    //在app.js中定义全局变量
  globalData: 'I am global data'
})
```

```javascript
//在page页面 **.js 使用全局变量
const appInstance = getApp()
console.log(appInstance.globalData) // I am global data
```


<!-- tabs:end -->