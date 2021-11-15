> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.setShadow** 用于设置阴影的位置和颜色。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961213843-71b266cf-6c8b-4a4e-a5e2-5d32af26843c.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624961228544-f4b5f45e-d769-4db0-a80d-5f77fb04e680.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const ctx = my.createCanvasContext('canvas')
ctx.setFillStyle('red')
ctx.setShadow(15, 45, 45, 'yellow')
ctx.fillRect(20, 20, 100, 175)
ctx.draw()
```

显示效果如下所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961243067-b3035eb5-e949-44f0-b686-86ef37064e28.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=32951&status=done&style=none&width=1280)

## 入参
**number offsetX**

阴影相对于形状水平方向的偏移。可选，默认值为 0。

**number offsetY**

阴影相对于形状竖直方向的偏移。可选，默认值为 0。

**number blur**

阴影的模糊级别，值越大越模糊。可选，取值范围为 0~100，默认值为 0。

**Color color**

阴影颜色。可选，默认值为 black。
