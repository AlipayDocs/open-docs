> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.rotate** 用于以原点为中心（原点可以用 [translate](https://opendocs.alipay.com/mini/api/lgqkb2) 方法修改），顺时针旋转当前坐标轴。多次调用 `rotate`，旋转的角度会叠加。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624935088421-07b9645a-7195-409c-96b4-cd519de72953.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624935095725-6c189cce-2b66-4e81-ad3a-cfc68af29804.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.strokeRect(200, 20, 180, 150)
ctx.rotate(30 * Math.PI / 180)
ctx.strokeRect(200, 20, 180, 150)
ctx.rotate(30 * Math.PI / 180)
ctx.strokeRect(200, 20, 180, 150)
ctx.draw()
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624935117677-3d10acea-9d87-4548-abba-ef117322e04a.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=35961&status=done&style=none&width=1280)

## 入参
**number rotate**

旋转角度，以弧度计(degrees * Math.PI/180；degrees 范围为 0~360 ) 。
