> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.createLinearGradient** 用于创建一个线性的渐变色。需要使用 [addColorStop()](https://opendocs.alipay.com/mini/api/addColorStop) 来指定渐变点，至少需要两个渐变点。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1626499387407-6b9d016f-47a6-4e99-aae0-c91eeb362d8c.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1626499393511-836ad06e-bafb-47f2-91db-7cec1997da7c.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
const grd = ctx.createLinearGradient(10, 10, 150, 10);
grd.addColorStop(0, 'yellow');
grd.addColorStop(1, 'blue');
ctx.setFillStyle(grd);
ctx.fillRect(20, 20, 250, 180);
ctx.draw();
```

## 入参

**number x0**

起点 x 坐标。

**number y0**

起点 y 坐标。

**number x1**

终点 x 坐标。

**number y1**

终点 y 坐标。

## 返回值

[CanvasGradient](https://opendocs.alipay.com/mini/api/CanvasGradient)
