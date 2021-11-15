> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.strokeRect** 用于画非填充矩形。

## 使用限制

- 用 `setFillStroke()` 设置矩形线条的颜色，如果没设置默认是 `black`。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962066711-f41c3a7c-6d80-4707-bda2-c7ea3c518634.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624962073458-e297a54f-9244-4ec7-9b11-0372be646e8d.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.setStrokeStyle('blue')
ctx.strokeRect(20, 20, 250, 80)
ctx.draw()
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962078067-039eea54-7ae7-4bd5-a3d3-02d0332fc4bb.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=24775&status=done&style=none&width=1280)

## 入参
**number x**

矩形左上角的 x 坐标。

**number y**

矩形左上角的 y 坐标。

**number width**

矩形路径宽度。

**number height**

矩形路径高度。
