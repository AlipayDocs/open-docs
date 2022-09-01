> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.draw** 用于将之前在绘图上下文中的描述（路径、变形、样式）画到 canvas 中。绘图上下文需要由 `my.createCanvasContext(canvasId)` 来创建。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874246599-4c5e9b03-4cd3-4026-9d5b-958ff340dfcb.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624874254002-6f62fd48-3fbc-45f3-adac-92bc5c2b9c2a.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### 示例代码 1

#### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.setFillStyle('blue');
ctx.fillRect(20, 20, 180, 80);
ctx.draw();
ctx.fillRect(60, 60, 250, 120);
// 保留上一次的绘制结果
ctx.draw(true);
```

显示效果如下图所示： ![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874283154-3bc8004d-5053-4ebe-a6e3-bd114f6fa49b.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=25866&status=done&style=none&width=1280)

### 示例代码 2

#### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.setFillStyle('blue');
ctx.fillRect(20, 20, 180, 80);
ctx.draw();
ctx.fillRect(60, 60, 250, 120);
// 不保留上一次的绘制结果
ctx.draw(false);
```

显示效果如下图所示： ![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874293666-38c5be8b-dee4-4ba8-8df7-f8fc0837b3f7.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=4.png&originHeight=720&originWidth=1280&size=27553&status=done&style=none&width=1280)

## 入参

**boolean reserve**

本次绘制是否接着上一次绘制。默认为 false。

- 若 reserve 参数为 `false` ，则在本次调用 drawCanvas 绘制之前 native 层应先清空画布再继续绘制。
- 若 reserver 参数为 `true` 时，则保留当前画布上的内容，本次调用 drawCanvas 绘制的内容覆盖在上面。

**function callback**

绘制完成后执行的回调函数。可选。
