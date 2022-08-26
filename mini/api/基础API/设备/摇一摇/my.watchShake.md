# 简介

**my.watchShake** 是摇一摇功能的 API。每次调用 API，在摇一摇手机后触发回调，如需再次监听则需要再次调用这个 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/91bd06bc9d534766dd9db04756169bd1.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/806b3529d4cd0d8d6c0649c864c1a7e6.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=none&width=746)

# 接口调用

## 示例代码

### .json 示例代码

```json
// API-DEMO page/API/watch-shake/watch-shake.json
{
  "defaultTitle": "Shake"
}
```

### .axml 示例代码

```html
<!-- API-DEMO page/API/watch-shake/watch-shake.axml-->
<view class="page">
  <button type="primary" onTap="watchShake">
    绑定摇一摇，点击 Shake 按钮看效果
  </button>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/watch-shake/watch-shake.js
Page({
  watchShake() {
    my.watchShake({
      success: function () {
        console.log('动起来了');
        my.alert({ title: '动起来了 o.o' });
      },
    });
  },
});
```
