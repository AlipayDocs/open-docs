> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.fillRect** 用于填充矩形。

`setFillStyle()` 用于设置矩形的填充色，如果没设置则默认是 `black`。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874935468-08f0bc06-fbcf-4535-ac0e-98bacef0ddea.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624874957691-1a5b6d4b-f729-40de-b51e-823d10a00a2f.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.fillRect(20, 20, 250, 80);
ctx.setFillStyle('blue');
ctx.draw();
```

显示效果如下图所示： ![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874978920-59417c6a-85cc-4d7f-9574-1942a615e322.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=24485&status=done&style=none&width=1280)

## 入参

**number x**

矩形左上角的 x 坐标。

**number y**

矩形左上角的 y 坐标。

**number width**

矩形路径宽度。

**number height**

矩形路径高度。
