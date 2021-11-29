
# 简介
停止监听设备方向变化事件。

## 使用限制

- 基础库 [1.12.0](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// page.js
Page({
  deviceMotionChangeListener(res) {
    console.log(res.alpha);
    console.log(res.beta);
    console.log(res.gamma);
  },
  onReady() {
    my.onDeviceMotionChange(this.deviceMotionChangeListener);
  },
  onUnload() {
    my.offDeviceMotionChange(this.deviceMotionChangeListener);
  }
})
```

## 入参

### function callback
设备方向变化事件的回调函数。

**注意**：若 my.offDeviceMotionChange 没有传入任何 `callback` 参数，则会取消监听所有的设备方向变化事件回调函数。
