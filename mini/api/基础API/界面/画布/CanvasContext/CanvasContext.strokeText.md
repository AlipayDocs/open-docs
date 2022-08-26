> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.strokeText** 是在给定的 *(x, y) *位置绘制文本的方法。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962066711-f41c3a7c-6d80-4707-bda2-c7ea3c518634.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=stroke&width=128)

# 调用

## 示例代码

### .js 示例代码

```javascript
const context = my.createCanvasContext('canvas');
context.font = 'italic bold 50px cursive';
context.strokeText('Hello world', 50, 100);
context.draw();
```

## 入参

**string text**

要绘制的文本。

**number x**

文本起始点的 x 轴坐标。

**number y**

文本起始点的 y 轴坐标。

**number maxWidth**

需要绘制的最大宽度，可选。
