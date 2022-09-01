> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.getImageData** 用于获取 canvas 区域隐含的像素数据。

## 使用限制

- 基础库 [1.10](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624875262323-a2da64b8-2ae9-42b6-8d6d-860494551aa8.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624875269708-3bcaa53a-927a-44cb-b0f0-700097723898.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
const ctx = my.createCanvasContext('canvas');
ctx.getImageData({
  x: 0,
  y: 0,
  width: 100,
  height: 100,
  success(res) {
    console.log(res.width); // 100
    console.log(res.height); // 100
    console.log(res.data instanceof Uint8ClampedArray); // true
    console.log(res.data.length); // 100 * 100 * 4
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| x | Number | 是 | 将要被提取的图像数据矩形区域的左上角横坐标。 |
| y | Number | 是 | 将要被提取的图像数据矩形区域的左上角纵坐标。 |
| width | Number | 是 | 将要被提取的图像数据矩形区域的宽度。 |
| height | Number | 是 | 将要被提取的图像数据矩形区域的高度。 |
| success | Function | 否 | 成功回调。 |
| fail | Function | 否 | 失败回调。 |
| complete | Function | 否 | 完成回调。 |

### success 回调函数

| **属性** | **类型** | **描述**             |
| -------- | -------- | -------------------- |
| width    | Number   | 图像数据矩形的宽度。 |
| height   | Number   | 图像数据矩形的高度。 |
