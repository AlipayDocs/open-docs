> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.createCircularGradient** 用于创建一个圆形的渐变色。起点在圆心，终点在圆环。需要使用 [addColorStop()](https://opendocs.alipay.com/mini/api/addColorStop) 来指定渐变点，至少需要两个渐变点。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624872611868-5ae94ddc-a7bd-4ca8-853f-320a6261eff3.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624872620305-8d9254a5-33a3-4e3a-9be1-e87b977078b8.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
const grd = ctx.createCircularGradient(90, 60, 60)
grd.addColorStop(0, 'blue')
grd.addColorStop(1, 'red')
ctx.setFillStyle(grd)
ctx.fillRect(20, 20, 250, 180)
ctx.draw()
```

显示效果如下图所示：

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624872631452-7345a8c8-b808-4ad2-897c-e5fb41256c06.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=36051&status=done&style=none&width=1280)

## 入参
**number x**

圆心 x 坐标。

**number y**

圆心 y 坐标。

**number r**

圆半径。

## 返回值
[CanvasGradient](https://opendocs.alipay.com/mini/api/CanvasGradient)
