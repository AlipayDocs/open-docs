> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.setTextAlign** 用于 Canvas 2D API 描述绘制文本时，设置文本的对齐方式。该对齐是基于 CanvasRenderingContext2D.fillText 方法的 x 的值。如果 textAlign="center"，那么该文本将画在 x-50%\*width 的位置。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961420956-08f0c184-ba80-4ed8-88a1-54f438cb59eb.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624961430325-8e9d1fb4-f444-48a2-a398-b15d8f2ab1ab.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
const ctx = my.createCanvasContext('canvas');
ctx.setStrokeStyle('red');
ctx.moveTo(150, 20);
ctx.lineTo(150, 170);
ctx.stroke();
ctx.setFontSize(15);
ctx.setTextAlign('left');
ctx.fillText('textAlign=left', 150, 60);
ctx.setTextAlign('center');
ctx.fillText('textAlign=center', 150, 80);
ctx.setTextAlign('right');
ctx.fillText('textAlign=right', 150, 100);
ctx.draw();
```

显示效果如下图所示： ![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961450186-00ec6051-783d-42c7-a071-7aaa16a83b6c.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=31092&status=done&style=none&width=1280)

## 入参

Object 类型，属性如下：

| **属性**  | **类型** | **描述**                                     |
| --------- | -------- | -------------------------------------------- |
| textAlign | String   | 可选取值为 left、right、center、start、end。 |
