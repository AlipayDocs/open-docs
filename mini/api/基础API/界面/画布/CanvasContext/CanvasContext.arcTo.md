> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.arcTo** 根据控制点和半径绘制圆弧路径。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962146631-2d9e47e9-40e8-4f38-a51e-a01d9bf60f46.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=stroke&width=128)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const context = my.createCanvasContext('canvas');

context.setLineDash([])
context.beginPath();
context.moveTo(150, 20);
context.arcTo(150, 100, 50, 20, 30);
context.stroke();

context.fillStyle = 'blue';
// base point
context.fillRect(150, 20, 10, 10);

context.fillStyle = 'red';
// control point one
context.fillRect(150, 100, 10, 10);
// control point two
context.fillRect(50, 20, 10, 10);

context.setLineDash([5,5])
context.moveTo(150, 20);
context.lineTo(150,100);
context.lineTo(50, 20);
context.stroke();
context.beginPath();
context.arc(120,38,30,0,2*Math.PI);
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

