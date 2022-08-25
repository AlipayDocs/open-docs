# 简介

**my.stopAccelerometer** 停止监听加速度数据。

## 使用限制

- 基础库 [1.24.9](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// page.js
Page({
  onReady() {
    this.accelerometerChangeCallback = function (res) {
      console.log(res.x);
      console.log(res.y);
      console.log(res.z);
    };
    my.startAccelerometer({
      interval: 'ui',
      success: () => {
        my.onAccelerometerChange(this.accelerometerChangeCallback);
      },
    });
  },
  onUnload() {
    my.stopAccelerometer({
      success: () => {
        my.offAccelerometerChange(this.accelerometerChangeCallback);
      },
    });
  },
});
```

## 入参

为 Object 类型。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | function | 否 | 接口调用成功的回调函数。 |
| fail | function | 否 | 接口调用失败的回调函数。 |
| complete | function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |
