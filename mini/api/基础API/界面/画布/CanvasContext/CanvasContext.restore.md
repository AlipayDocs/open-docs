> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.restore** 用于恢复之前保存的绘图上下文。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624934525098-9f7a2d4b-72c7-43ed-afef-2d0a8d1321a3.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624934531559-267cc16e-642c-4b60-ad7e-6683f6bbad8f.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```
//.js
const ctx = my.createCanvasContext('canvas');
ctx.save();
ctx.setFillStyle('red');
ctx.fillRect(20, 20, 250, 80);
ctx.restore();
ctx.fillRect(60, 60, 155, 130);
ctx.draw();
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624934560701-07b8365f-1f8e-430e-bb97-604d6af9a1a4.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=28369&status=done&style=none&width=1280)
