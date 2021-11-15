> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.beginPath** 是开始创建一个路径，需要调用 `fill` 或者 `stroke` 才会使用路径进行填充或描边。 在创建路径最开始时，相当于调用了一次 `beginPath()`，同一个路径内的多次 `setFillStyle()`、`setStrokeStyle()`、`setLineWidth()` 等设置，以最后一次设置为准。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624870616136-6320c382-3913-4a05-a7f3-d414c9812abb.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=CanvasContext.beginPath%E2%80%94%E2%80%941.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624870625059-a0f8f75d-3b05-4c8b-b700-7b5efac502d9.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=CanvasContext.beginPath%E2%80%94%E2%80%942.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=none&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.rect(20, 20, 150, 50)
ctx.setFillStyle('blue')
ctx.fill();
ctx.beginPath();
ctx.rect(20, 50, 150, 40)
ctx.setFillStyle('yellow')
ctx.fillRect(20, 170, 150, 40)
ctx.rect(10, 100, 100, 30)
ctx.setFillStyle('red')
ctx.fill()
ctx.draw()
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624870647106-5caf63e5-3d8f-4358-8b30-bc779367683a.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=CanvasContext.beginPath%E2%80%94%E2%80%943.png&originHeight=720&originWidth=1280&size=26599&status=done&style=none&width=1280)

