> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.setLineJoin** 用于设置线条的交点样式。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624959781100-efa5400a-ab1f-4c3e-a6e1-6dde909a7349.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624959790335-de92102e-f09b-446c-8552-394263b0f6ef.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.beginPath()
ctx.moveTo(10, 10)
ctx.lineTo(100, 50)
ctx.lineTo(10, 90)
ctx.stroke()
ctx.beginPath()
ctx.setLineJoin('bevel')
ctx.setLineWidth(10)
ctx.moveTo(50, 10)
ctx.lineTo(140, 50)
ctx.lineTo(50, 90)
ctx.stroke()
ctx.beginPath()
ctx.setLineJoin('round')
ctx.setLineWidth(10)
ctx.moveTo(90, 10)
ctx.lineTo(180, 50)
ctx.lineTo(90, 90)
ctx.stroke()
ctx.beginPath()
ctx.setLineJoin('miter')
ctx.setLineWidth(10)
ctx.moveTo(130, 10)
ctx.lineTo(220, 50)
ctx.lineTo(130, 90)
ctx.stroke()
ctx.draw()
```

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624959850029-64ba288a-2e76-4bd1-9ce0-f167741a1143.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=31617&status=done&style=none&width=1280)

## 入参
**string lineJoin**

线条的结束交点样式。

### lineJoin 的合法值
| **值** | **说明** |
| --- | --- |
| round | 圆角。 |
| bevel | 斜角。 |
| miter | 尖角。 |

