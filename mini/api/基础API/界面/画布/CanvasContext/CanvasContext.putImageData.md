> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.putImageData** 用于将像素数据绘制到画布。

## 使用限制

基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624933843777-ab0f8efc-ec1b-416e-9a69-95831923c838.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624933851813-9bec2df2-c90a-43ba-9078-1cb5a6e61ea1.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=none&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
const data = new Uint8ClampedArray([255, 0, 0, 1]);
const ctx = my.createCanvasContext('canvas');
ctx.putImageData({
  x: 0,
  y: 0,
  width: 1,
  height: 1,
  data: data,
  success(res) {},
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| data | Uint8ClampedArray | 是 | 图像像素点数据，一维数组，每四项表示一个像素点的 rgba。 |
| x | Number | 是 | 源图像数据在目标画布中的位置偏移量（x 轴方向的偏移量）。 |
| y | Number | 是 | 源图像数据在目标画布中的位置偏移量（y 轴方向的偏移量）。 |
| width | Number | 是 | 源图像数据矩形区域的宽度 。 |
| height | Number | 是 | 源图像数据矩形区域的高度。 |
| success | Function | 否 | 成功回调。 |
| fail | Function | 否 | 失败回调。 |
| complete | Function | 否 | 完成回调。 |
