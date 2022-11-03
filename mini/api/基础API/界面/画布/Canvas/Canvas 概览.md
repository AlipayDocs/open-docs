> 相关文档：[旧版 Canvas 迁移指南](https://opendocs.alipay.com/mini/055eid)

## 简介
Canvas 实例，可以通过 [SelectorQuery](https://opendocs.alipay.com/mini/api/pc8s51) 获取。

## 使用限制

- **基础库** [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。


## 基础示例

.axml 示例代码

```html
<!-- 必须指定 type，否则无法获取到 context -->
<canvas id="canvas" type="2d" onReady="onCanvasReady"></canvas>
```

如果您的项目中已使用类似 `<canvas id="canvas"></canvas>` 这样未指定 type 的标签，可以参考 [旧版 Canvas 迁移指南](https://opendocs.alipay.com/mini/055eid) 替换。


.js 示例代码
```js
Page({
    // 一定要在 canvas 的 onReady 中调用，否则获取到的 context 可能不正确
    onCanvasReady() {
        // 通过 SelectorQuery 获取 Canvas 实例
        my.createSelectorQuery().select('#canvas').node().exec((res) => {
                const canvas = res[0].node;
                const ctx = canvas.getContext('2d');
                console.log('canvas 宽高', canvas.width, canvas.height)

                // 开始绘画
                ctx.fillRect(0, 0, 50, 50);
            });
    },
});
```


## 属性

| **属性** | **类型** | **描述**   |
| -------- | -------- | ---------- |
| width    | Number   | 画布宽度。 |
| height   | Number   | 画布高度。 |

## 方法

| **名称** | **描述** |
| --- | --- |
| [Canvas.getContext](https://opendocs.alipay.com/mini/api/getcontext) | 返回 Canvas 的绘制上下文。 |
| [Canvas.createImage](https://opendocs.alipay.com/mini/api/createimage) | 创建图片对象，支持 2DCanvas 和 WebGL Canvas 使用。 |
| [Canvas.requestAnimationFrame](https://opendocs.alipay.com/mini/api/requestAnimationFrame) | 帧调用，下次重绘之前调用指定的回调函数。 |
| [Canvas.cancelAnimationFrame](https://opendocs.alipay.com/mini/api/cancelAnimationFrame) | 取消 requestAnimationFrame 添加的动画帧请求。 |
| [Canvas.toTempFilePath](https://opendocs.alipay.com/mini/api/toTempFilePath) | 把当前画布指定区域的内容导出生成指定大小的图片。 |

# 常见问题 FAQ
## Q：Canvas 文档里内容看起来很少，我该怎么知道所有 API？
A：查看 [RenderingContext](https://opendocs.alipay.com/mini/01w0it) 介绍。RenderingContex 和 web 标准对齐，因此完整 API 可以参考 MDN 文档。
