# 简介

**my.createOffscreenCanvas** 创建离屏 Canvas 实例。

## 使用限制

- 基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。

# 接口调用

## 示例代码

### .axml 示例代码
```html
<canvas id="canvas" type="2d" onReady="onCanvasReady"></canvas>
```

### .js 示例代码
```js
Page({
    onCanvasReady() {

        const self = this;
        my.createSelectorQuery().select('#canvas').node().exec((res) => {
            const canvas = res[0].node;
            const ctx = canvas.getContext('2d');
            self.canvas = canvas;
            self.ctx = ctx;

            self.draw();
        });

    },

    // 创建离屏 canvas，填充自定义像素数据，然后画到 canvas 中
    draw() {
        const ctx = this.ctx;

        // 创建离屏 canvas
        const offCanvas = my.createOffscreenCanvas(20, 20);
        const offCtx = offCanvas.getContext('2d');

        // RenderingContext 对齐 web 标准，因此 createImageData 可直接参考 MDN。
        const imageData = offCtx.createImageData(20, 20);
        const data = imageData.data;

        let pixelCount = offCanvas.width * offCanvas.height;
        // 遍历离屏 canvas 中的每个像素，设置其 R、G、B、A 值
        for (let i = 0; i < pixelCount * 4; i += 4) {
            // R
            data[i + 0] = 190;
            // G
            data[i + 1] = 0;
            // B
            data[i + 2] = 210;
            // A
            data[i + 3] = 255;
        }

        // 将自定义的像素数据填充进离屏 canvas 上下文中。putImageData 可以直接参考 MDN。
        offCtx.putImageData(imageData, 0, 0);

        // 将离屏 canvas 里的数据画到 canvas 里。
        ctx.drawImage(offCanvas, 100, 60);
        ctx.drawImage(offCanvas, 100, 100, 100, 100);

    },

});

```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |
| width | Number | 否 | 画布宽度。默认为 100。 |
| height | Number | 否 | 画布高度。默认为 100。 |

## 返回值

可查看 [OffscreenCanvas](https://opendocs.alipay.com/mini/api/021yfb)。
