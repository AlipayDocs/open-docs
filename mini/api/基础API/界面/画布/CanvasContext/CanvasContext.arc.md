# 简介

CanvasContext.arc 用于创建一个弧线路径。
- 创建一个实心圆形可以指定起始弧度为 0，终止弧度为 `2 * Math.PI` ，并用 `fill()` 填充。
- 用 `stroke()` 方法在 canvas 中画弧线。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624870278082-cad25ceb-7aca-4c74-beb5-f18b8d35796d.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=CanvasContext.arc_1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624870286071-494b5944-7f95-4e6a-ab85-c3cf19ee255b.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=CanvasContext.arc%E2%80%94%E2%80%942.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=none&width=300)

# 调用

## 示例代码

### .js 示例代码

```javascript
const ctx = my.createCanvasContext('canvas')

// 画一个圆形并填充颜色
ctx.arc(100, 75, 50, 0, 2 * Math.PI)
ctx.setFillStyle('#EEEEEE')
ctx.fill()

// 画一个十字
ctx.beginPath()
ctx.moveTo(40, 75)
ctx.lineTo(160, 75)
ctx.moveTo(100, 15)
ctx.lineTo(100, 135)
ctx.setStrokeStyle('#AAAAAA')
ctx.stroke()

// 画文字
ctx.setFontSize(12)
ctx.setFillStyle('black')
ctx.fillText('0', 165, 78)
ctx.fillText('0.5*PI', 83, 145)
ctx.fillText('1*PI', 15, 78)
ctx.fillText('1.5*PI', 83, 10)

// 画上绿、蓝、红三个小圆形
ctx.beginPath()
ctx.arc(100, 75, 2, 0, 2 * Math.PI)
ctx.setFillStyle('lightgreen')
ctx.fill()

ctx.beginPath()
ctx.arc(100, 25, 2, 0, 2 * Math.PI)
ctx.setFillStyle('blue')
ctx.fill()

ctx.beginPath()
ctx.arc(150, 75, 2, 0, 2 * Math.PI)
ctx.setFillStyle('red')
ctx.fill()


// 画一段弧线
ctx.beginPath()
ctx.arc(100, 75, 50, 0, 1.5 * Math.PI)
ctx.setStrokeStyle('#333333')
ctx.stroke()

ctx.draw()
```

显示效果如下图所示： ![CanvasContext.arc——3.png](https://cdn.nlark.com/yuque/0/2021/png/179989/1624870323606-4fefc202-3917-42bc-8f92-952d9bcde979.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=CanvasContext.arc%E2%80%94%E2%80%943.png&originHeight=720&originWidth=1280&size=29072&status=done&style=none&width=1280)

针对 arc(100, 75, 50, 0, 1.5 \* Math.PI) 的三个关键坐标如下：

- 绿色: 圆心 (100, 75)。
- 红色: 起始弧度 (0)。
- 蓝色: 终止弧度 (1.5 \* Math.PI)。

## 入参

**number x** 圆 x 坐标。

**number y**

圆 y 坐标。

**number r**

圆半径。

**number sAngle**

起始弧度，单位弧度（在 3 点钟方向）。

**number eAngle**

终止弧度。

**boolean counterclockwise**

指定弧度的方向是逆时针还是顺时针，可选，默认为 false。
