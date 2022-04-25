# 简介

**my.vibrateShort** 是调用触发较短时间的振动（40ms）的 API。

## 使用限制

- 仅在 iPhone 7 / 7 Plus 以上及 Android 机型生效。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/518bb55b663b8731712655304e29e917.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fe3dc6a33cb0d79b1d79283ec88c4c42.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

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
  <button type="primary" onTap="vibrate">
    开始振动
  </button>
  <button type="primary" onTap="vibrateLong">
    长时间振动 (400ms)
   </button>
  <button type="primary" onTap="vibrateShort">
    短时间振动 (40ms)
  </button>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/vibrate/vibrate.js
Page({
  vibrate() {
    my.vibrate({
      success: () => {
        my.alert({ title: '振动起来了'});
      }
    });
  },
  vibrateLong() {
    if (my.canIUse('vibrateLong')) {
      my.vibrateLong((res) => { });
    } else {
      my.alert({
        title: '客户端版本过低',
        content: 'my.vibrateLong() 需要 10.1.35 及以上版本'
      });
    }
  },
  vibrateShort() {
    if (my.canIUse('vibrateShort')) {
      my.vibrateShort((res) => { });
    } else {
      my.alert({
        title: '客户端版本过低',
        content: 'my.vibrateShort() 需要 10.1.35 及以上版本'
      });
    }
  }
});
```
