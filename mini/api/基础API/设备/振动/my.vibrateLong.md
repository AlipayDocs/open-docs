# 简介

**my.vibrateLong** 是调用触发较长时间的振动（400ms）的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5bfebd220003eb791db3c6918e54b814.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/49414b61c24e9b44545b83e68e76393f.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .json 示例代码

```json
// API-DEMO page/API/vibrate/vibrate.json
{
  "defaultTitle": "Vibrate"
}
```

### .axml 示例代码

```html
<!-- API-DEMO page/API/vibrate/vibrate.axml-->
<view class="page">
  <button type="primary" onTap="vibrate">开始振动</button>
  <button type="primary" onTap="vibrateLong">长时间振动 (400ms)</button>
  <button type="primary" onTap="vibrateShort">短时间振动 (40ms)</button>
</view>
```

### .js 示例代码

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
