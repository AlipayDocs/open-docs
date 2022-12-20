## 使用说明
- 通过页面跳转（my.navigateTo）或者页面重定向（my.redirectTo）所到达的页面，即使它是定义在 tabBar 配置中的页面，也不会显示底部的 tab 栏。
- tabBar 的第一个页面必须是首页，即 app.json-pages 中配置的第一个小程序页面。
- tabBar 的 icon 暂不支持 gif 动画。
- 小程序 tabBar、titleBar 多语言配置目前仅支持 zh-Hans（简体中文）、zh-Hant（繁体中文台湾）、zh-HK（繁体中文香港）、en（英文）四种语言。
- 在非 tabbar 页面跳转至 tabbar 页使用 my.reLaunch 跳转；tabbar 页之间跳转使用 my.switchTab 跳转。
- tabbar 最多支持配置五个导航页面。

## 常见问题

### 小程序tabbar页面如何透出消息提示
可查看 [小程序tabbar页面如何透出消息提示](https://opendocs.alipay.com/support/01rb29)。

### 动态设置tabBar
小程序提供了动态设置 tabBar 的 API：[my.setTabBarStyle](https://opendocs.alipay.com/mini/api/wcf0sv)。<br />可以根据场景需要动态设置 tabBar 整体样式，动态设置 item 可使用 [my.setTabBarItem](https://opendocs.alipay.com/mini/api/zu37bk)。

### tabBar的图标推荐大小
tabBar的图标 icon 和 activeIcon 推荐大小为 60 * 60px，系统会对任意传入的图片非等比拉伸/缩放。

### tabbar是否支持设置字体大小
支付宝小程序 tabbar 不支持设置字体大小。

### 底Bar的border颜色设置
底部 Bar 的 border 颜色目前不能设置，tabbar 没有 border 的属性进行设置。

### 小程序tabBar和titleBar多语言配置
[小程序 tabBar、titleBar 多语言配置](https://opendocs.alipay.com/mini/framework/vivu3s)：

- 语言统一放到根目录下的 locale 目录下。
- 每个语言一个目录，如 zh-Hans（简体中文）、zh-HK （繁体中文香港）。
- 在每个语言目录下，通过添加 app.json 配置，配置该语言下的 titleBar 与 tabBar。

**注意：** 目前仅支持 zh-Hans（简体中文）、zh-Hant（繁体中文台湾）、zh-HK（繁体中文香港）、en（英文）四种语言。<br />
配置示例：
```json
// locale/zh-Hans/app.json 
{  
   "window": {  
     "defaultTitle": "测试"   
   },   
   "tabBar": {     
     "items": [  
       {    
         "name": "列表" 
       },    
       {     
         "name": "一"   
       },     
       {     
         "name": "二"    
       }    
     ]   
   },  
   "pages": {  
     "pages/index/index": {   
       "defaultTitle": "首页"  
     }  
   } 
 }
```

### tabBar的icon支持哪些图片格式
设置tabbar上的 icon 只支持 png/jpeg/jpg/gif 图片格式，不支持 svg 格式；支持在线图片 URL。

### tabBar切换时对应页面的onShow会不会触发
tabBar页面切换时对应的页面会触发 onShow 函数。

### 跳转页面后不显示tabBar
通过页面跳转 my.navigateTo 或者页面重定向 my.redirectTo 所到达的页面，即使它是定义在 tabBar 配置中的页面，也不会显示底部的 tab 栏。另外，tabBar 的第一个页面必须是首页。

### 配置tabBar右上角文本
可以使用以下API：

- my.setTabBarBadge 对tabBar某一项右上角添加文本。
- my.removeTabBarBadge 对tabBar某一项右上角添加的文本进行移除。

**注意：** 基础库版本 1.11.0 开始支持为 tabBar 某一项的右上角添加文本。<br />
详情可查看 [my.setTabBarBadge](https://opendocs.alipay.com/mini/api/qm7t3v)、[my.removeTabBarBadge](https://opendocs.alipay.com/mini/api/lpbp5g)。

### 如何监听tabbar点击事件？
在小程序页面中用 [onTabitemTap](https://opendocs.alipay.com/mini/api/navg36) 即可监听 TabBar 点击事件。<br />
**注意：基础库** [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；**支付宝客户端** 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。<br />
示例代码：
```javascript
//.js
Page({  
  onTabItemTap(item) {  
    console.log(item.index)  
    console.log(item.pagePath)
    console.log(item.text) 
  }
})
```

### TabBar页面不支持带参数跳转吗
TabBar 页面目前不支持带参跳转，建议跳转传参使用缓存或者全局变量。

### 蒙层能否遮住小程序导航栏和tabBar
蒙层不能遮住小程序导航栏和 tabBar。蒙层实现可查看扩展组件 [Mask 背景蒙层](https://opendocs.alipay.com/mini/component-ext/mask)。

### 小程序tabBar可以控制隐藏或显示吗
小程序提供API：

- 隐藏tabBar：[my.hideTabBary](https://opendocs.alipay.com/mini/api/at18z8)
- 显示tabBar：[my.showTabBar](https://opendocs.alipay.com/mini/api/dpq5dh)

### 如何动态设置tabBar某一项的内容
小程序提供了动态设置tabBar某一项的内容的API：[my.setTabBarItem](https://opendocs.alipay.com/mini/api/zu37bk)；可以根据场景需要动态设置 tabBar 某一项的内容。<br />
**说明：** 图片路径，建议尺寸为 81px * 81px，支持网络图片。

### 在showLoading情况下，是否会禁止tab切换

- 在 my.showLoading 情况下，显示 loading 后，会覆盖整个 H5 页面，页面元素不能交互。
- 在 my.showLoading 情况下，不会禁止 tab 切换，可以正常切换 tabBar。

### 普通关联二维码扫码进入小程序后底部tabbar导航栏不显示
是普通关联二维码的配置的路径 /pages/index/index 有误导致，应改为 pages/index/index，需去掉最前面的/。

### 使用my.navigateTo或者my.redirectTo跳转的页面为什么不显示底部的tab栏
通过页面跳转 [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) 或者页面重定向 [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 所到达的页面，即使它是定义在 tabBar 配置中的页面，也不会显示底部的 tab 栏。若要跳转到 tab 页面，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) 方法。

### 切换TabBar时报错Cannot read property &#39;getCurrentPages&#39; of undefined如何处理
tabbar 路径错误导致，请检查 tabbar 路径。
