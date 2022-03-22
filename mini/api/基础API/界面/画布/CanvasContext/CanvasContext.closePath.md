> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.closePath** 用于关闭一个路径。关闭路径会连接起点和终点。如果关闭路径后没有调用 `fill()` 或者 `stroke()` 并开启了新的路径，那之前的路径将不会被渲染。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624872172538-7ab50a00-2377-4a07-a09f-a028b9c2b08e.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624872182257-f938c3be-9410-427f-8e7c-8e1b4950ef23.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
示例代码 1：
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.moveTo(20, 20)
ctx.lineTo(150, 20)
ctx.lineTo(150, 150)
ctx.closePath()
ctx.stroke()
ctx.draw()
```

显示效果如下图所示：

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624872196806-d199b5be-c55f-49fe-b1f4-0388cdb14a94.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=28578&status=done&style=none&width=1280)

示例代码 2：
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.rect(20, 20, 150, 50)
ctx.closePath()
ctx.beginPath()
ctx.rect(20, 50, 150, 40)
ctx.setFillStyle('red')
ctx.fillRect(20, 80, 120, 30)
ctx.rect(20, 150, 150, 40)
ctx.setFillStyle('blue')
ctx.fill()
ctx.draw()
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624872221547-a3ef4d23-384d-410d-b20b-51ec5d06b55e.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=4.png&originHeight=720&originWidth=1280&size=27203&status=done&style=none&width=1280)

