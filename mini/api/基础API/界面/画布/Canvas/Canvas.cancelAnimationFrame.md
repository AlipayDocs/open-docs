# 简介

**Canvas.cancelAnimationFrame** 用于取消有 requestAnimationFrame 添加的动画帧请求。支持在 2D Canvas 和 WebGL Canvas 下使用。

## 使用限制

- 基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码

```html
<!-- canvas.axml -->
<canvas type="2d" id="canvas" onReady="onCanvasReady"></canvas>
```

### .js 示例代码

```javascript
// canvas.js
Page({
  onCanvasReady() {
    const query = my.createSelectorQuery();
    query
      .select('#canvas')
      .node()
      .exec(res => {
        const canvas = res[0].node;
        const ctx = canvas.getContext('2d');
        var requestId = canvas.requestAnimationFrame(() => {
          ctx.fillStyle = 'red';
          ctx.fillRect(0, 0, 50, 50);
        });
        canvas.cancelAnimationFrame(requestId);
      });
  },
});
```

## 入参

number requestID
