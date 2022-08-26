> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.drawImage** 用于绘制图像，图像保持原始尺寸。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874573899-d33d5c08-a608-4ccf-8fe2-a15f79b7db56.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624874585045-6fa3a71f-acd8-43c7-b2a6-f0a1620705b3.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
const ctx = my.createCanvasContext('canvas');
ctx.drawImage(
  'https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg',
  2,
  2,
  250,
  80
);
ctx.draw();
```

显示效果如下图所示： ![|738x415](https://cdn.nlark.com/yuque/0/2021/png/179989/1624874618092-dd24ae65-9e5e-4c34-b2d7-49a51c4bf5e1.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&name=3.png&originHeight=720&originWidth=1280&size=58657&status=done&style=none&width=1280)

## 入参

**string imageResource**

图片资源。支持 Base64 格式、线上 cdn 地址或离线包地址，线上 cdn 需返回头 `Access-Control-Allow-Origin: *`。

**number x**

图像左上角 x 坐标。

**number y**

图像左上角 y 坐标 。

**number width**

图像宽度。

**number height**

图像高度。
