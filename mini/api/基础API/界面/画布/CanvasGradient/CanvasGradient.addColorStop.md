
# 简介
**CanvasGradient.addColorStop** 用于添加颜色的渐变点。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![](https://cdn.nlark.com/yuque/0/2021/png/179989/1624870278082-cad25ceb-7aca-4c74-beb5-f18b8d35796d.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=stroke&width=128)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
// 创建圆形梯度色
const grd = ctx.createLinearGradient(30, 10, 120, 10)
grd.addColorStop(0, 'red')
grd.addColorStop(0.16, 'orange')
grd.addColorStop(0.33, 'yellow')
grd.addColorStop(0.5, 'green')
grd.addColorStop(0.66, 'cyan')
grd.addColorStop(0.83, 'blue')
grd.addColorStop(1, 'purple')
// 填充梯度色
ctx.setFillStyle(grd)
ctx.fillRect(10, 10, 150, 80)
ctx.draw()
```


显示效果如下图所示：<br />![](https://cdn.nlark.com/yuque/0/2021/png/179989/1624875400424-f5bad4a3-b8bd-4eb6-a974-126a23fda999.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=none&width=1280)

## 入参
**number stop**<br />表示渐变中开始与结束之间的位置，范围 0-1。<br />**Color color**<br />渐变点的颜色。
