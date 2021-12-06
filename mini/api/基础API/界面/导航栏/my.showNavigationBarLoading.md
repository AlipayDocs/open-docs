
# 简介
**my.showNavigationBarLoading** 是在当前页面显示导航条的加载动画的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fe6407a4eed43ead11e42b331564d3a0.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-navigation-bar-loading?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
    "defaultTitle": "标题栏加载动画"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/navigation-bar-loading/navigation-bar-loading.axml-->
<view class="page">
  <view class="page-section">
    <button type="primary" onTap="showNavigationBarLoading">显示加载动画</button>
    <button onTap="hideNavigationBarLoading">隐藏加载动画</button>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/navigation-bar-loading/navigation-bar-loading.js
Page({
  showNavigationBarLoading() {
    my.showNavigationBarLoading()
  },
  hideNavigationBarLoading() {
    my.hideNavigationBarLoading()
  }
})
```

### .acss 示例代码
```css
/* API-DEMO page/API/navigation-bar-loading/navigation-bar-loading.acss */
button + button {
  margin-top: 20rpx;
}
```
