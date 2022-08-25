# 简介

监听设备方向变化，目前回调频率为 200ms/次 左右。

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
  },
});
```

## 入参

### function callback

设备方向变化事件的回调函数。

#### callback 参数

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| alpha | Number | 当手机坐标 X/Y 和 地球 X/Y 重合时，绕着 Z 轴转动的夹角为 alpha，范围值为 [0, 2\*PI)。逆时针转动为正。 |
| beta | Number | 当手机坐标 Y/Z 和地球 Y/Z 重合时，绕着 X 轴转动的夹角为 beta。范围值为 [-1\*PI, PI) 。顶部朝着地球表面转动为正。也有可能朝着用户为正。 |
| gamma | Number | 当手机 X/Z 和地球 X/Z 重合时，绕着 Y 轴转动的夹角为 gamma。范围值为 [-1\*PI/2, PI/2)。右边朝着地球表面转动为正。 |
