> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.quadraticCurveTo** 用于创建二次贝塞尔曲线路径。曲线的起始点为路径中前一个点。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624934060809-f00961be-d4ef-4dca-955f-fbf60dac6e85.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624934069686-e1bd8c4d-1743-4adb-9ca8-86a112af2c51.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=none&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.beginPath()
ctx.arc(30, 30, 2, 0, 2 * Math.PI)
ctx.setFillStyle('red')
ctx.fill()
ctx.beginPath()
ctx.arc(250, 20, 2, 0, 2 * Math.PI)
ctx.setFillStyle('blue')
ctx.fill()
ctx.beginPath()
ctx.arc(30, 200, 2, 0, 2 * Math.PI)
ctx.setFillStyle('green')
ctx.fill()
ctx.setFillStyle('black')
ctx.setFontSize(12)
ctx.beginPath()
ctx.moveTo(30, 30)
ctx.lineTo(30, 150)
ctx.lineTo(250, 30)
ctx.setStrokeStyle('#AAAAAA')
ctx.stroke()
ctx.beginPath()
ctx.moveTo(30, 30)
ctx.quadraticCurveTo(30, 150, 250, 25)
ctx.setStrokeStyle('black')
ctx.stroke()
ctx.draw()
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624934044536-f9bf0ffa-5790-4988-a407-9d2f75eddb85.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=29856&status=done&style=none&width=1280)

针对 `moveTo(30, 30)quadraticCurveTo(30, 150, 250, 25)` 的三个关键坐标如下：

- 红色：起始点(30, 30)
- 蓝色：控制点(30, 150)
- 绿色：终止点(250, 25)

## 入参
**number cpx**

贝塞尔控制点 x 坐标。

**number cpy**

贝塞尔控制点 y 坐标。

**number x**

结束点 x 坐标。

**number y**

结束点 y 坐标。
