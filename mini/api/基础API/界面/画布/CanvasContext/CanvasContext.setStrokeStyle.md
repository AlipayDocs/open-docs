> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.setStrokeStyle** 用于设置边框颜色。若没有设置，则默认颜色为 `black`。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961180687-5d1851dc-db61-4685-af14-24a19629455c.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624961187945-9dd96923-5ec7-4f8a-8df7-2be781b349f6.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
const ctx = my.createCanvasContext('canvas');
ctx.setStrokeStyle('blue');
ctx.strokeRect(50, 50, 100, 175);
ctx.draw();
```

显示效果如下图所示：

![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961193469-6e6a8ab7-fd05-4962-82f1-50bb500047ef.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=23833&status=done&style=none&width=1280)

## 入参

**Color color**

颜色。
