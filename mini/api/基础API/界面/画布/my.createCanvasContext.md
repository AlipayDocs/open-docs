
# 简介
> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，本接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

**my.createCanvasContext** 是创建 [canvas](https://opendocs.alipay.com/mini/component/canvas) 绘图上下文的 API。该绘图上下文只作用于对应 `canvasId` 的 `<canvas/>` 。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/os/skylark-tools/public/files/4d18af844e5f9fa0ae404619b252542a.jpeg%26originHeight%3D158%26originWidth%3D128%26size%3D20015%26status%3Ddone%26width%3D128#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=none&width=128)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/examples/14e91d68-3c09-43ce-8904-0fb8f04dbd7b) 

## 入参
**string canvasId**<br />定义在 `<canvas/>` 上的 ID。

## 返回值
返回值为 [CanvasContext](https://opendocs.alipay.com/mini/api/canvascontext)。
