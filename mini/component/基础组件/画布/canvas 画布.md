# 简介

画布是一个矩形区域，用于在页面上绘制图形、动画，开发者可以控制其中的每一个像素。Canvas 拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。

基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持新版 Canvas。新版 Canvas 支持同层渲染，使用时必须指定 type 属性和 onReady 事件。相关 API 可查看 [获取 Canvas 实例](https://opendocs.alipay.com/mini/01vzqv)。

如果您的项目中已使用类似 `<canvas id="canvas"></canvas>` 这样未指定 type 的标签，请参考 [旧版 Canvas 迁移指南](https://opendocs.alipay.com/mini/055eid) 。



## 属性说明

| **属性**       | **类型**    | **描述**                                                     |
| -------------- | ----------- | ------------------------------------------------------------ |
| id             | String      | 组件唯一标识符。<br />**注意**：同一页面中的 id 不可重复。   |
| type           | String      | 类型。设置 type 属性后，会渲染成 native canvas。<br />**可选值**：2d、webgl<br />**版本要求**：基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onReady        | EventHandle | canvas 组件初始化成功事件。<br />**版本要求**：基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| width          | String      | 画布宽度。**默认值：** 300px                                 |
| height         | String      | 画布高度。**默认值：** 225px                                 |
| style          | String      | -                                                            |
| class          | String      | -                                                            |
| disable-scroll | Boolean     | 禁止屏幕滚动以及下拉刷新。<br />**默认值：** false           |
| onTap          | EventHandle | 点击事件。                                                   |
| onTouchStart   | EventHandle | 触摸动作开始事件。                                           |
| onTouchMove    | EventHandle | 触摸后移动事件。                                             |
| onTouchEnd     | EventHandle | 触摸动作结束事件。                                           |
| onTouchCancel  | EventHandle | 触摸动作被打断，如来电提醒，弹窗事件。                       |
| onLongTap      | EventHandle | 长按 500ms 之后触发，触发了长按事件后进行移动将不会触发屏幕的滚动。 |



# 使用

### Canvas2D

```html
<!-- .axml 必须指定 type，否则创建的将是旧版 Canvas -->
<canvas id="canvas" type="2d" onReady="onCanvasReady"></canvas>
```

```javascript
// .js
Page({

    onCanvasReady() {
        my.createSelectorQuery().select('#canvas').node().exec((res) => {
            const canvas = res[0].node
            const ctx = canvas.getContext('2d')

            const img = canvas.createImage()
            img.src = 'https://mdn.alipayobjects.com/huamei_esgcm9/afts/img/A*vlKfQKOGboQAAAAAAAAAAAAADsaJAQ/original'
            img.onload = () => {
                ctx.drawImage(img, 10, 10, 100, 100)
            }
        })

    },

})
```

### WebGL

```html
<!-- .axml 必须指定 type，否则创建的将是旧版 Canvas -->
<canvas type="webgl" id="canvas" onReady="onCanvasReady"></canvas>
```

```javascript
Page({
    onCanvasReady() {
        my.createSelectorQuery().select('#canvas').node().exec(res => {
            const canvas = res[0].node
            const gl = canvas.getContext('webgl')
            gl.clearColor(1, 1, 0, 1)
            gl.clear(gl.COLOR_BUFFER_BIT)
        })
    },
})
```

### Bug & Tip

- 使用新版 Canvas 必须指定 type 类型。

- 必须在 Canvas 组件的 onReady 回调函数中获取 canvas 实例和上下文。

- 若要在高 DPR（devicePixelRatio）下取得更细腻的显示，可以设置较大的画布大小，然后用样式等比例缩小组件。例如：

  ```html
  <canvas width="200" height="200" style="width:100px;height:100px;"></canvas>
  ```

  



# 附录：原生 Canvas 组件适配

## 简介

为了提升性能、优化小程序体验，新版 Canvas 基于原生组件实现。若在 iOS 平台遇到覆盖于 Canvas 组件上的 web 元素（后称：覆盖元素）无法收到 UI 事件时，可以进行如下适配。

#### 使用限制

- 基础库版本 2.7.0 及以上。
- 支付宝版本 10.2.0 及以上。

## 方法

1. 向小程序 app.json 的 `window` 中添加 `"enableComponentOverlayer":"YES"` 。

```json
{
	  "pages":[
		  "pages/index/index"
	  ],
	  "window":{
		  "enableComponentOverlayer":"YES"
	  }
  }
```

2. 为覆盖元素添加 `AF-COMPONENT-OVERLAYER` class 属性，使小程序将事件派发给覆盖元素，而不传递给后边的 Canvas 组件。

```css
/* 设置 z-index 使元素覆盖在 Canvas 上 */
.top {
  z-index: 2;
}
```

```html
<view class="page">
  <canvas style="width: 100%; height: 500px;"></canvas>
  <!-- view 元素覆盖在 Canvas 上方，在 class 中添加 "AF-COMPONENT-OVERLAYER" 即可接收到 UI 事件 -->
  <view class="top AF-COMPONENT-OVERLAYER" onTap="viewClick"></view>
</view>
```

**注意：** 若在开发中遇到 Canvas 组件上没有可见的 web 元素覆盖（即 axml 文件中无覆盖元素）时也收不到 UI 事件，可以只采用步骤 1。这会使小程序运行时将目标区域内 UI 事件派发给 Canvas 组件。
