> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.createRadialGradient** 用于创建一个放射性的渐变色。需要使用 [addColorStop()](https://opendocs.alipay.com/mini/api/addColorStop)来指定渐变点，至少需要两个渐变点。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624872611868-5ae94ddc-a7bd-4ca8-853f-320a6261eff3.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=stroke&width=128)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
const grd = ctx.createRadialGradient(100, 100, 100, 100, 100, 0);
grd.addColorStop(0, 'white');
grd.addColorStop(1, 'green');
ctx.setFillStyle(grd);
ctx.fillRect(20, 20, 250, 180);
ctx.draw();
```

## 入参

**number x0**

开始圆形的 x 轴坐标。

**number y0**

开始圆形的 y 轴坐标。

**number r0**

开始圆形的半径。

**number x1**

结束圆形的 x 轴坐标。

**number y1**

结束圆形的 y 轴坐标。

**number r1**

结束圆形的半径。
