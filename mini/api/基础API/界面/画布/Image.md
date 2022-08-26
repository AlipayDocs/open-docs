# 简介

**Image** 是图片对象，当调用 [Canvas.createImage](https://opendocs.alipay.com/mini/api/createimage) 方法时返回此对象。

## 使用限制

- 基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
var ctx = canvas.getContext('2d');
var img = canvas.createImage();
img.src = 'https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg';
img.onload = function () {
  console.log('load image success');
  ctx.drawImage(img, 0, 0);
};
img.onerror = function (err) {
  console.log('load image err');
};
```

## 属性

| **属性** | **类型** | **描述**                           |
| -------- | -------- | ---------------------------------- |
| src      | String   | 图片的 URL。                       |
| width    | Number   | 图片的真实宽度。                   |
| height   | Number   | 图片的真实高度。                   |
| onload   | Function | 图片加载完成时触发的回调函数。     |
| onerror  | Function | 图片加载发生错误时触发的回调函数。 |
