# 简介

**my.onUserCaptureScreen** 是用于监听用户发起的主动截屏事件的 API。可以接收到系统以及第三方截屏工具的截屏事件通知。可使用 [my.offUserCaptureScreen()](https://opendocs.alipay.com/mini/api/umdxbg) 取消监听。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a3ab9d583f22223740b8907d9e2d06b1.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/251ee50771d061c43bfc5d0eef79995c.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

### .axml 示例代码

```html
<!-- API-DEMO page/API/user-capture-screen/user-capture-screen.axml-->
<view class="page">
  <view class="page-description">用户截屏事件 API</view>
  <view class="page-section">
    <view class="page-section-title">my.onUserCaptureScreen</view>
    <view class="page-section-demo">
      <view>目前状态：{{ condition ? "已经开启监听" : '已经取消监听' }}</view>
      <view a:if="{{condition}}">
        <button type="primary" onTap="offUserCaptureScreen">
          取消监听屏幕事件
        </button>
      </view>
      <view a:else>
        <button type="primary" onTap="onUserCaptureScreen">
          开启监听屏幕事件
        </button>
      </view>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/user-capture-screen/user-capture-screen.js
Page({
  data: {
    condition: false,
  },
  onReady() {
    my.onUserCaptureScreen(() => {
      my.alert({
        content: '收到用户截图',
      });
    });
  },
  offUserCaptureScreen() {
    my.offUserCaptureScreen();
    this.setData({
      condition: false,
    });
  },
  onUserCaptureScreen() {
    my.onUserCaptureScreen(() => {
      my.alert({
        content: '收到用户截图',
      });
    });
    this.setData({
      condition: true,
    });
  },
});
```
