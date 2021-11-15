> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.clearRect** 用于清除画布上在该矩形区域内的内容。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624871392293-062318e5-31d9-4731-a792-aaceaee8a25b.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624871404954-f6fb5c28-146c-4225-b16c-6380f9c36195.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=none&width=300)

# 接口调用

## 示例代码
clearRect 并非画一个白色的矩形在地址区域，而是清空，为了有直观感受，可以对 canvas 加一层背景色。

### .axml 示例代码
```html
//.axml
<canvas id="canvas" style="border: 1px solid; background: red;"/>
```


### .js 示例代码
```javascript
// .js
const ctx = my.createCanvasContext('canvas')
ctx.setFillStyle('blue')
ctx.fillRect(250, 10, 250, 200)
ctx.setFillStyle('yellow')
ctx.fillRect(0, 0, 150, 200)
ctx.clearRect(10, 10, 150, 75)
ctx.draw()
```

## 入参
**number x**

矩形左上角的 x 坐标。

**number y**

矩形左上角的 y 坐标。

**number width**

矩形宽度。

**number height**

矩形高度。
