> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.setFontSize** 用于设置字体大小。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624936238725-e34897ef-8df4-4bc5-a231-44404f17d36b.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624936247772-38fac4e4-de89-42a9-9f94-b030a550777d.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.setFontSize(14)
ctx.fillText('14', 20, 20)
ctx.setFontSize(22)
ctx.fillText('22', 40, 40)
ctx.setFontSize(30)
ctx.fillText('30', 60, 60)
ctx.setFontSize(38)
ctx.fillText('38', 90, 90)
ctx.draw()
```

显示效果如下图所示：

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624936276528-b864fc21-ac4a-4adf-9ef4-7832a0181b39.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=27651&status=done&style=none&width=1280)

## 入参
**number fontSize**

字号。
