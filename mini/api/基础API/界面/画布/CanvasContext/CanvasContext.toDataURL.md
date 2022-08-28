> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

# 简介

**CanvasContext.toDataURL** 用于获取画布指定区域的 data URL 数据。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962146631-2d9e47e9-40e8-4f38-a51e-a01d9bf60f46.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624962154430-fbb1cce6-1b45-4c36-9909-c59acc53942e.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
const ctx = my.createCanvasContext('canvas');
ctx.setFillStyle('#108ee9');
ctx.arc(50, 50, 50, 0, Math.PI * 2, true);
ctx.fill();
ctx.draw(false, () => {
  ctx
    .toDataURL({
      x: 50,
      y: 50,
      width: 50,
      height: 50,
      destWidth: 100,
      destHeight: 100,
    })
    .then(dataURL => {
      ctx.drawImage(dataURL, 0, 0);
      ctx.draw();
    });
});
```

## 入参

**number x**

将要被提取的矩形区域的左上角横坐标。可选，默认值为 0。

**number y**

将要被提取的矩形区域的左上角纵坐标。可选，默认值为 0。

**number width**

将要被提取的矩形区域的宽度。可选，默认值为被提取的矩形区域的左上角到画布右下角的横向距离。

**number height**

将要被提取的矩形区域的高度。可选，默认值为被提取的矩形区域的左上角到画布右下角的纵向距离。

**number destWidth**

将要被提取的矩形区域提取后的宽度。可选，默认等于 width。

**number destHeight**

将要被提取的矩形区域提取后的高度。可选，默认等于 height。

**string fileType**

图片格式，可选值为 jpg 或 png。可选，默认为 png。

**number quality**

图片格式为 jpg 的情况下，data URL 对应的图片的质量。取值范围为 0 到 1，如果超出取值范围，将会默认该值为 1。其他图片格式该参数会被忽略。

## 返回值

**Promise<string>**

提取的 dataURL 字符串。
