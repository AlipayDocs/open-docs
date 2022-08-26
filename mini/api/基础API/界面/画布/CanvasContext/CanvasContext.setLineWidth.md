> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.setLineWidth** 用于设置线条的宽度。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624960085185-0e55ee7f-49af-4e62-a211-34e15e28f28e.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624960095121-3da390a2-4a41-4f0d-bf27-a33f97f41255.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.beginPath();
ctx.moveTo(10, 10);
ctx.lineTo(150, 10);
ctx.stroke();
ctx.beginPath();
ctx.setLineWidth(5);
ctx.moveTo(10, 30);
ctx.lineTo(150, 30);
ctx.stroke();
ctx.beginPath();
ctx.setLineWidth(10);
ctx.moveTo(10, 50);
ctx.lineTo(150, 50);
ctx.stroke();
ctx.beginPath();
ctx.setLineWidth(15);
ctx.moveTo(10, 70);
ctx.lineTo(150, 70);
ctx.stroke();
ctx.draw();
```

显示效果如下所示： ![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624960186911-322cb7ed-03a3-417c-9be7-18cc5f3c4300.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=24221&status=done&style=none&width=1280)

## 入参

**number lineWidth**

线条宽度，单位为 px。
