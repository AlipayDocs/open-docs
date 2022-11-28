> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

> 相关文档：[旧版 Canvas 迁移指南](https://opendocs.alipay.com/mini/055eid)

# 简介

**CanvasContext.arcTo** 根据基础点、控制点和半径，绘制圆弧路径。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962146631-2d9e47e9-40e8-4f38-a51e-a01d9bf60f46.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=stroke&width=128)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 这是一段绘制圆弧的简单的代码片段。基础点是蓝色的，两个控制点是红色的。
const context = my.createCanvasContext('canvas');

// 绘制切线
context.beginPath();
context.strokeStyle = 'gray';
context.moveTo(200, 20);
context.lineTo(200, 130);
context.lineTo(50, 20);
context.stroke();

// 绘制起始点
context.beginPath();
context.fillStyle = 'blue';
context.arc(200, 20, 5, 0, 2 * Math.PI);
context.fill();

// 绘制控制点
context.beginPath();
context.fillStyle = 'red';
// 控制点 1
context.arc(200, 130, 5, 0, 2 * Math.PI);
// 控制点 2
context.arc(50, 20, 5, 0, 2 * Math.PI);
context.fill();

// 绘制弧线
context.beginPath();
context.strokeStyle = 'black';
context.lineWidth = 5;
context.moveTo(200, 20);
context.arcTo(200,130, 50,20, 40);
context.stroke();

context.draw()
```

## 入参

**number x1**

第一个控制点的 x 轴坐标。

**number y1**

第一个控制点的 y 轴坐标。

**number x2**

第二个控制点的 x 轴坐标。

**number y2**

第二个控制点的 y 轴坐标。

**number radius**

圆弧的半径。
