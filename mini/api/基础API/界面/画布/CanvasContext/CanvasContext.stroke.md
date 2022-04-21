> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介
**CanvasContext.stroke** 用于画出当前路径的边框。

## 使用限制

- `stroke()` 描绘的路径是从 `beginPath()` 开始计算，但是不会将 `strokeRect()` 包含进去，可查看示例代码 2。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961889901-00f42425-3258-4f4f-9a68-eeef2d26ac1c.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624961900326-ff472f6f-3992-40e8-9132-0dcdb59cf1a5.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
示例代码 1：
```javascript
const ctx = my.createCanvasContext('canvas')
ctx.moveTo(10, 10)
ctx.lineTo(100, 10)
ctx.lineTo(100, 100)
ctx.stroke()
ctx.draw()
```

显示效果如下图所示：

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961915322-78a5f406-c226-4349-a4a7-73f2d9b948de.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=24657&status=done&style=none&width=1280)

示例代码 2：
```javascript
const ctx = my.createCanvasContext('canvas');
ctx.rect(10, 10, 100, 30)
ctx.setStrokeStyle('yellow')
ctx.stroke()
ctx.beginPath()
ctx.rect(10, 40, 100, 30)
ctx.setStrokeStyle('blue')
ctx.strokeRect(10, 70, 100, 30)
ctx.rect(10, 100, 100, 30)
ctx.setStrokeStyle('red')
ctx.stroke()
ctx.draw()
```

显示效果如下所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961931805-d98278c8-c773-4eb3-ba46-16044e67065e.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=4.png&originHeight=720&originWidth=1280&size=26715&status=done&style=none&width=1280)

