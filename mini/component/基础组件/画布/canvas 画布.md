这篇文档讲解了在支付宝小程序中如何使用 Canvas 组件进行图形和动画的绘制。文档首先介绍了 Canvas 的基本概念和功能，然后提到自基础库 2.7.0 起，新版 Canvas 支持同层渲染，并指出使用时需指定 type 属性和 onReady 事件，并提供了相关 API 的链接。文档接着提醒如果在项目中已使用未指定 type 的旧版 canvas 标签，应参考迁移指南进行更新。最后，文档详细列出了 Canvas 组件的属性说明，并对每个属性进行了描述，包括其类型、描述、默认值、版本要求，并特别指出了某些属性的适用条件和判断依据。
# 使用 Canvas2D

```html
<!-- .axml 中必须指定 type，否则创建的将是旧版 Canvas -->
<canvas id="canvas" type="2d" onReady="onCanvasReady"></canvas>
```

```javascript
// .js
Page({

    onCanvasReady() {
        my.createSelectorQuery().select('#canvas').node().exec((res) => {
            const canvas = res[0].node;
            const ctx = canvas.getContext('2d');

            const img = canvas.createImage();
            img.src = 'https://mdn.alipayobjects.com/huamei_esgcm9/afts/img/A*vlKfQKOGboQAAAAAAAAAAAAADsaJAQ/original';
            img.onload = () => {
                ctx.drawImage(img, 10, 10, 100, 100);
            }
        });

    },

});
```
### WebGL

```html
<!-- .axml 文件中必须指定 type 为 webgl，否则将创建旧版本的 Canvas -->
<canvas type="webgl" id="canvas" onReady="onCanvasReady"></canvas>
```

```javascript
Page({
    onCanvasReady() {
        my.createSelectorQuery().select('#canvas').node().exec(res => {
            const canvas = res[0].node;
            const gl = canvas.getContext('webgl');
            gl.clearColor(1, 1, 0, 1);
            gl.clear(gl.COLOR_BUFFER_BIT);
        });
    },
});
```

### Bug & Tip

- 使用新版 Canvas 时，必须明确指定 `type` 属性的类型。
- `onReady` 回调函数中，需要获取 Canvas 组件的实例和上下文。
- 如需在高 DPI 设备上获得更清晰的显示效果，应设置较大的 Canvas 画布尺寸，并通过样式缩小组件比例。例如：

  ```html
  <canvas width="200" height="200" style="width: 100px; height: 100px;"></canvas>
  ```
# 附录：原生 Canvas 组件适配

## 简介

为了提升性能、优化小程序体验，新版 Canvas 基于原生组件实现。若在 iOS 平台遇到覆盖于 Canvas 组件上的 web 元素（后称：覆盖元素）无法收到 UI 事件时，可以进行如下适配。

#### 使用限制

- 基础库版本 2.7.0 及以上。
- 支付宝版本 10.2.0 及以上。

## 方法

1. 向小程序 `app.json` 的 `window` 中添加 `"enableComponentOverlayer":"YES"`。

```json
{
    "pages": [
        "pages/index/index"
    ],
    "window": {
        "enableComponentOverlayer": "YES"
    }
}
```

2. 为覆盖元素添加 `AF-COMPONENT-OVERLAYER` 类属性，使小程序将事件派发给覆盖元素，而不传递给后面的 Canvas 组件。

```css
/* 设置 z-index，使元素覆盖在 Canvas 上 */
.top {
    z-index: 2;
}
```

```html
<view class="page">
    <canvas style="width: 100%; height: 500px;"></canvas>
    <!-- 在 class 中添加 "AF-COMPONENT-OVERLAYER"，使该 view 元素能够覆盖在 Canvas 上方并接收到 UI 事件 -->
    <view class="top AF-COMPONENT-OVERLAYER" onTap="viewClick"></view>
</view>
```

**注意：** 若在开发中遇到 Canvas 组件上没有可见的 web 元素覆盖（即 AXML 文件中无覆盖元素）时也收不到 UI 事件，可以只采用步骤 1。这会让小程序在运行时将目标区域内的 UI 事件派发给 Canvas 组件。
