
# 简介
**Canvas.createImage** 用于创建一个图片对象。支持 2D Canvas 和 WebGL Canvas下使用。

## 使用限制

- 基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码
```html
<!-- canvas.axml -->
<canvas type="2d"  id="canvas" onReady="onCanvasReady"></canvas>
```

### .js 示例代码
```javascript
// canvas.js
Page({
  onCanvasReady() {
    const query = my.createSelectorQuery();
      query.select('#canvas').node().exec((res) => {
      const canvas = res[0].node;
        const ctx = canvas.getContext('2d');
        const img = canvas.createImage();
        img.src = "https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg";
        img.onload = () => {
          ctx.drawImage(img, 10, 10, 100, 100);
      }
    })
  }
})
```

## 返回值
返回值为 [Image](https://opendocs.alipay.com/mini/01vyku)。
