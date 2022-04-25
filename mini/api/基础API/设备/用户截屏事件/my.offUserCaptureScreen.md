# 简介

**my.offUserCaptureScreen** 是用于取消监听截屏事件的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5d1e486d074cdcad0206fdfd113f753f.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b0f0b81ff9c0a27cd1621a532b7e18f5.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

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
        <button type="primary" onTap="offUserCaptureScreen">取消监听屏幕事件</button>
      </view>
      <view a:else>
        <button type="primary" onTap="onUserCaptureScreen">开启监听屏幕事件</button>
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
        content: '收到用户截图'
      });
    });
    this.setData({
      condition: true,
    });
  },
});
```

## 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件回调。示例代码如下：
```javascript
my.offUserCaptureScreen();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：
```javascript
my.offUserCaptureScreen(this.callback);
```
