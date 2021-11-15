> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.fill** 用于对当前路径中的内容进行填充。默认的填充色为黑色。

## 使用限制

- 如果当前路径没有闭合，`fill()` 方法会将起点和终点进行连接，然后填充，详情见 **示例代码 1**。
- fill() 填充的的路径从 `beginPath()` 开始计算，但不包含 `fillRect()` ，详情见 **示例代码 2**。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874794446-0e299fcd-3a6f-4709-b7f3-5451baabe664.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624874803895-3e6430f5-20d6-4a09-89df-2432ee03dde3.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### 示例代码 1

#### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.moveTo(20, 20)
ctx.lineTo(200, 20)
ctx.lineTo(200, 200)
ctx.fill()
ctx.draw()
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874815125-a77df7b3-412c-46a0-bfef-3d0064e984d6.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=31499&status=done&style=none&width=1280)

### 示例代码 2

#### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.rect(20, 20, 110, 40)
ctx.setFillStyle('blue')
ctx.fill()
ctx.beginPath()
ctx.rect(20, 30, 150, 40)
ctx.setFillStyle('yellow')
ctx.fillRect(20, 80, 150, 40)
ctx.rect(20, 150, 150, 40)
ctx.setFillStyle('red')
ctx.fill()
ctx.draw()
```

显示效果如下图所示：

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874830894-0f3d6c28-94ed-4941-b3b7-7ad820f53c85.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=4.png&originHeight=720&originWidth=1280&size=28990&status=done&style=none&width=1280)
