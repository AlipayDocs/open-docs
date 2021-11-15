> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.measureText** 用于测量文本尺寸信息，目前仅返回文本宽度。为同步接口。

## 使用限制

- 调用此方法获取到的文本宽度是设备的像素值，因 Android 系统和 iOS 系统两端字体处理方式不同，导致实际的返回值会存在一定的差异，建议在各自系统上做兼容处理。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624933262879-f7e812aa-3d41-48a2-8a6e-a75ff25e3164.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624933270448-0cbf0747-2e9a-4c10-ae47-0a1a02edac0e.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2%E3%80%91.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const ctx = my.createCanvasContext('canvas')
ctx.font = 'italic bold 50px cursive'
const { width } = ctx.measureText('hello world')
console.log(width)
```

## 入参
**string text**

要测量的文本。

## 返回值
返回 TextMetrics 对象，结构如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| width | Number | 文本的宽度，为设备的像素值。<br />**注意**：因 Android 系统和 iOS 系统两端字体处理方式不同，导致实际的返回值会存在一定的差异，建议在各自系统上做兼容处理。 |

