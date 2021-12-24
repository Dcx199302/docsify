



## 一、起步

- [注册开发者账号](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/getstart.html#%E7%94%B3%E8%AF%B7%E5%B8%90%E5%8F%B7)

## 二、目录结构

<!-- tabs:start -->

#### **目录结构**

```javascript
/**
* 小程序主体部分文件组成
* app.js
* app.wxss
* app.json
*
* 页面组成
* js
* wxml
* wxss
* json
*/
```

### **文件白名单**

```html
在项目目录中: { .js、app.json、.wxml、*.wxss } 会经过编译、因此上传之后无法直接访问这些文件

下面为白名单文件，非白名单的文件在开发工具即使能访问，也不能上传
wxs、png、jpg、jpeg、gif、svg、json、cer、
mp3、aac、m4a、mp4、wav、ogg、silk、wasm、br、
```

### **小程序局限**

- **小程序框架的逻辑层并非运行在浏览器中，因此 `JavaScript` 在 web 中一些能力都无法使用，如 `window`，`document` 等。**

<!-- tabs:end -->



## 三、配置小程序

<!-- tabs:start -->

### **全局配置**

- [小程序全局配置](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html)

```json
//小程序根目录下的 app.json 文件用来对微信小程序进行全局配置
//决定页面文件的路径、窗口表现、设置网络超时时间、设置多 tab 等。
{
  "pages": [
    "pages/index/index",
    "pages/logs/index"
  ],
  "window": {
    "navigationBarTitleText": "Demo"
  },
  "tabBar": {
    "list": [{
      "pagePath": "pages/index/index",
      "text": "首页"
    }, {
      "pagePath": "pages/logs/index",
      "text": "日志"
    }]
  },
  "networkTimeout": {
    "request": 10000,
    "downloadFile": 10000
  },
  "debug": true
}
```



### **页面配置**

- [小程序页面配置](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/page.html)

- 每一个小程序页面也可以使用同名 `.json` 文件来对本页面的窗口表现进行配置，页面中配置项会覆盖 `app.json` 的 `window` 中相同的配置项。

  ```json
  {
    "navigationBarBackgroundColor": "#ffffff",
    "navigationBarTextStyle": "black",
    "navigationBarTitleText": "微信接口功能演示",
    "backgroundColor": "#eeeeee",
    "backgroundTextStyle": "light"
  }
  ```

### **sitemap 配置**

- 配置了才能被微信小程序搜索
- 小程序根目录下的 `sitemap.json` 文件用于配置小程序及其页面是否允许被微信索引，文件内容为一个 JSON 对象，如果没有 `sitemap.json` ，则默认为所有页面都允许被索引
- [sitemap配置](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/sitemap.html)

<!-- tabs:end -->

