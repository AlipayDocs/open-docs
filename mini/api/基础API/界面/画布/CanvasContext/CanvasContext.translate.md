> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.translate** 是对当前坐标系的原点（0, 0）进行变换，默认的坐标系原点为页面左上角。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962430747-2fbf145c-3ef8-4589-8014-f77e682bb2ab.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624962437387-d27d44ae-d1bd-4a3f-a989-9da8e2d033bb.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.strokeRect(20, 20, 250, 80);
ctx.translate(30, 30);
ctx.strokeRect(20, 20, 250, 80);
ctx.translate(30, 30);
ctx.strokeRect(20, 20, 250, 80);
ctx.draw();
```

显示效果如下图所示：

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962453007-2133b54a-b320-41e5-82af-57cab6b36040.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=33925&status=done&style=none&width=1280)

## 入参

**number x**

水平坐标平移量。

**number y**

竖直坐标平移量。
