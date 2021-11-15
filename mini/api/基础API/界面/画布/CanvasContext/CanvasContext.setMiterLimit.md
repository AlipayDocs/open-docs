> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.setMiterLimit** 用于设置最大斜接长度，斜接长度指的是在两条线交汇处内角和外角之间的距离。 仅当 `setLineJoin()` 为 `miter` 时有效。超过最大倾斜长度的，连接处将以 `lineJoin` 为 bevel 显示。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624960713075-0d611b96-b8b9-44ae-ace8-82ae699e95ba.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624960720656-c0ba30b5-1c55-479b-bab2-234161411c13.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.beginPath()
ctx.setLineWidth(15)
ctx.setLineJoin('miter')
ctx.setMiterLimit(1)
ctx.moveTo(10, 10)
ctx.lineTo(100, 50)
ctx.lineTo(10, 90)
ctx.stroke()
ctx.beginPath()
ctx.setLineWidth(15)
ctx.setLineJoin('miter')
ctx.setMiterLimit(2)
ctx.moveTo(50, 10)
ctx.lineTo(140, 50)
ctx.lineTo(50, 90)
ctx.stroke()
ctx.beginPath()
ctx.setLineWidth(15)
ctx.setLineJoin('miter')
ctx.setMiterLimit(3)
ctx.moveTo(90, 10)
ctx.lineTo(180, 50)
ctx.lineTo(90, 90)
ctx.stroke()
ctx.draw()
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624960739633-785a3305-67aa-4c76-a2c5-c0d861975f9d.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=34224&status=done&style=none&width=1280)

## 入参
**number miterLimit**

最大斜接长度。
