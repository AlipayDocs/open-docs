> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.setTransform** 是使用单位矩阵重新设置（覆盖）当前的变换并调用变换的方法，此变换由方法的变量进行描述。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961708941-94e59d9b-5bf9-46e1-a75d-1ad8edb28030.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624961717497-706a435e-46d1-4839-a17b-aa6cd132b135.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.rotate((45 * Math.PI) / 180);
ctx.setFillStyle('red');
ctx.fillRect(70, 0, 100, 30);
ctx.setTransform(1, 1, 0, 1, 0, 0);
ctx.setFillStyle('#000');
ctx.fillRect(0, 0, 100, 100);
ctx.draw();
```

显示效果如下图所示： ![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961732154-ea1a10c3-007f-40f2-a110-af954894f4e1.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=30004&status=done&style=none&width=1280)

## 入参

**number scaleX**

水平缩放。

**number skewX**

水平倾斜。

**number skewY**

垂直倾斜。

**number scaleY**

垂直缩放。

**number translateX**

水平移动。

**number translateY**

垂直移动。
