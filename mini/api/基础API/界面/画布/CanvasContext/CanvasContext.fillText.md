> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.fillText** 用于在画布上绘制被填充的文本。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624875098340-de7b28ef-eaa0-43f9-8e97-632b6b64c2bd.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624875109938-9b0759ce-f52a-4d9d-b3b0-b38c567cdd29.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.setFontSize(42)
ctx.fillText('Hello', 30, 30)
ctx.fillText('alipay', 200, 200)
ctx.draw()
```

显示效果如下图所示：

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624875128885-24578f92-6180-4646-81b1-f9d3d1a6a36b.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=29599&status=done&style=none&width=1280)

## 入参
**string text**

文本。

**number x**

绘制文本的左下角 x 坐标。

**number y**

绘制文本的左下角 y 坐标。
