# 简介

**my.vibrate** 是调用振动功能的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ef60fe69d0f066e01c171c02d2eec43d.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/1b088109b3b17c547c06e1bea139a4f7.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

```json
// API-DEMO page/API/vibrate/vibrate.json
{
  "defaultTitle": "Vibrate"
}
```

```html
<!-- API-DEMO page/API/vibrate/vibrate.axml-->
<view class="page">
  <button type="primary" onTap="vibrate">开始振动</button>
  <button type="primary" onTap="vibrateLong">长时间振动 (400ms)</button>
  <button type="primary" onTap="vibrateShort">短时间振动 (40ms)</button>
</view>
```

```javascript
// API-DEMO page/API/vibrate/vibrate.js
Page({
  vibrate() {
    my.vibrate({
      success: () => {
        my.alert({ title: '振动起来了' });
      },
    });
  },
  vibrateLong() {
    if (my.canIUse('vibrateLong')) {
      my.vibrateLong(res => {});
    } else {
      my.alert({
        title: '客户端版本过低',
        content: 'my.vibrateLong() 需要 10.1.35 及以上版本',
      });
    }
  },
  vibrateShort() {
    if (my.canIUse('vibrateShort')) {
      my.vibrateShort(res => {});
    } else {
      my.alert({
        title: '客户端版本过低',
        content: 'my.vibrateShort() 需要 10.1.35 及以上版本',
      });
    }
  },
});
```
