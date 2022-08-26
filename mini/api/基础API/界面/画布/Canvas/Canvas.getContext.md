# 简介

**Canvas.getContext** 用于返回 Canvas 的绘制上下文。

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
        ctx.fillStyle = 'red';
        ctx.fillRect(0, 0, 50, 50);
      });
  },
});
```

## 入参

### string contextType

绘图上下文类型。

#### contextType 合法值

| **值** | **说明**         |
| ------ | ---------------- |
| webgl  | webgl 类型上下文 |
| 2d     | 2d 类型上下文    |

## 返回值

返回值为 [RenderingContext](https://opendocs.alipay.com/mini/01w0it)。支持获取 2D Canvas 和 WebGL Canvas 绘制上下文。
