> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.setLineDash** 用于设置虚线的样式。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624936973060-bde34327-60ed-41b5-bd1c-723d6af49d59.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624936980384-8ba19b3a-27b7-45bc-beac-76f063c57314.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
const ctx = my.createCanvasContext('canvas')
ctx.setLineDash([10, 20], 5)
ctx.beginPath()
ctx.moveTo(0,100)
ctx.lineTo(400, 100)
ctx.stroke()
ctx.draw()
```

显示效果如下：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624936986466-d699e54e-99b4-455e-b879-f2df9b4b49ba.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=28689&status=done&style=none&width=1280)

## 入参
**Array<number> segments**

一组用于描述交替绘制线段和间距（坐标空间单位）长度的数字。 如果数组元素的数量是奇数， 数组的元素会被复制并重复。例如， [5, 15, 25] 会变成 [5, 15, 25, 5, 15, 25]。
