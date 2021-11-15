> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.setTextBaseline** 用于设置当前文本基线的属性。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961637976-f40f85fe-cbf4-4d31-bf86-e1750a5db24a.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624961631315-27d2d580-8a96-483f-bf88-587fad2fa95a.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.setStrokeStyle('red')
ctx.moveTo(5, 75)
ctx.lineTo(295, 75)
ctx.stroke()
ctx.setFontSize(20)
ctx.setTextBaseline('top')
ctx.fillText('top', 5, 75)
ctx.setTextBaseline('middle')
ctx.fillText('middle', 50, 75)
ctx.setTextBaseline('bottom')
ctx.fillText('bottom', 120, 75)
ctx.setTextBaseline('normal')
ctx.fillText('normal', 200, 75)
ctx.draw()
```

显示效果如下图所示：
![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624961621380-94fd0c16-4d08-467b-bcaa-bf30a9b560e3.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=30441&status=done&style=none&width=1280)

## 入参
**string textBaseline**

Canvas 2D API 描述绘制文本时，当前文本基线的属性。即文字垂直方向的对齐方式。默认 `alphabetic`。

### textBaseline 的合法值
| **值** | **说明** |
| --- | --- |
| top | 文本基线在文本块的顶部 |
| hanging | 文本基线是悬挂基线 |
| middle | 文本基线在文本块的中间 |
| alphabetic | 文本基线是标准的字母基线 |
| ideographic | 文字基线是表意字基线；如果字符本身超出了alphabetic 基线，那么ideograhpic基线位置在字符本身的底部。 |
| bottom | 本基线在文本块的底部 |
