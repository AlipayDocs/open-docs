> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.transform** 是使用矩阵多次叠加当前变换的方法，矩阵由方法的参数进行描述。可以缩放、旋转、移动和倾斜上下文。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962319475-13c92c7a-515d-40d8-8b55-5c857af5b6c6.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624962328332-9fd34968-a44a-42b4-81eb-2c05f22eb19f.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.rotate((45 * Math.PI) / 180);
ctx.setFillStyle('red');
ctx.fillRect(70, 0, 100, 30);
ctx.transform(1, 1, 0, 1, 0, 0);
ctx.setFillStyle('#000');
ctx.fillRect(0, 0, 100, 100);
ctx.draw();
```

显示效果如下图所示：

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624962347358-de9cc6e8-3a2a-48dc-bc1a-14411aafd191.gif#align=left&display=inline&height=362&margin=%5Bobject%20Object%5D&name=3.gif&originHeight=362&originWidth=298&size=50516&status=done&style=stroke&width=298)

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
