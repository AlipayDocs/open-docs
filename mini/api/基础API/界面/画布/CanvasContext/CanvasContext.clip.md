> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介
**CanvasContext.clip** 用于将当前创建的路径设置为当前剪切路径。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624872020579-b2f91ddb-b2c7-479e-8c58-b2cde8f5996a.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624872029032-3253c5f0-e6e0-45ef-b033-7060319d4d87.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
my.downloadFile({
  url: 'https://gw.alipayobjects.com/zos/skylark-tools/public/files/dda114e320567e1d304790287d75a029.png',
  success({ apFilePath }) {
    ctx.save()
    ctx.beginPath()
    ctx.arc(50, 50, 25, 0, 2 * Math.PI)
    ctx.clip()
    ctx.drawImage(apFilePath, 25, 25)
    ctx.restore()
    ctx.draw()
  }
})
```
