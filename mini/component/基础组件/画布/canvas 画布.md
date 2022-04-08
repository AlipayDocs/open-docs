# 简介
画布。画布是一个矩形区域，用于在页面上绘制图形，开发者可以控制其每一像素。canvas 拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。

基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持新的 Canvas 接口（需指定 type 属性）。相关 API 可查看 [获取 Canvas 实例](https://opendocs.alipay.com/mini/01vzqv)。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark/78b29ccd-ea8f-4537-b65c-e6a36d8d32c7/2018/jpeg/b0d9bbad-b532-4773-bd4a-8b330b070b26.jpeg#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-canvas?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### Canvas2D
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

### WebGL
```css
<!-- canvas.axml -->
<canvas type="webgl"  id="canvas" onReady="onCanvasReady"></canvas>
```


```javascript
Page({
  onCanvasReady() {
    const query = my.createSelectorQuery();
      query.select('#canvas').node().exec((res) => {
      const canvas = res[0].node;
        const gl = canvas.getContext('webgl');
        gl.clearColor(1, 1, 0, 1);
        gl.clear(gl.COLOR_BUFFER_BIT);
    })
  }
})
```

### 旧版接口 
相关 API：[my.createCanvasContext](https://opendocs.alipay.com/mini/api/ui-canvas)。

```html
<!-- API-DEMO page/component/canvas/canvas.axml -->
<view class="page">
  <view class="canvas-view">
    <canvas 
      id="canvas"
      width="610"
      height="610"
      class="canvas"
      onTouchStart="log"
      onTouchMove="log"
      onTouchEnd="log"
    />
  </view>
</view>
```

```javascript
// API-DEMO page/component/canvas/canvas.js
Page({
  onReady() {
    this.point = {
      x: Math.random() * 590,
      y: Math.random() * 590,
      dx: Math.random() * 10,
      dy: Math.random() * 10,
      r: Math.round(Math.random() * 255 | 0),
      g: Math.round(Math.random() * 255 | 0),
      b: Math.round(Math.random() * 255 | 0),
    };
    this.interval = setInterval(this.draw.bind(this), 17);
    this.ctx = my.createCanvasContext('canvas');
  },
  draw() {
    const { ctx } = this;
    ctx.setFillStyle('#FFF');
    ctx.fillRect(0, 0, 610, 610);
    ctx.beginPath();
    ctx.arc(this.point.x, this.point.y, 20, 0, 2 * Math.PI);
    ctx.setFillStyle('rgb(' + this.point.r + ', ' + this.point.g + ', ' + this.point.b + ')');
    ctx.fill();
    ctx.draw();
    this.point.x += this.point.dx;
    this.point.y += this.point.dy;
    if (this.point.x <= 10 || this.point.x >= 590) {
      this.point.dx = -this.point.dx;
      this.point.r = Math.round(Math.random() * 255 | 0);
      this.point.g = Math.round(Math.random() * 255 | 0);
      this.point.b = Math.round(Math.random() * 255 | 0);
    }
    if (this.point.y <= 10 || this.point.y >= 590) {
      this.point.dy = -this.point.dy;
      this.point.r = Math.round(Math.random() * 255 | 0);
      this.point.g = Math.round(Math.random() * 255 | 0);
      this.point.b = Math.round(Math.random() * 255 | 0);
    }
  },
  drawBall() {
  },
  log(e) {
    if (e.touches && e.touches[0]) {
      console.log(e.type, e.touches[0].x, e.touches[0].y);
    } else {
      console.log(e.type);
    }
  },
  onUnload() {
    clearInterval(this.interval);
  },
});
```

```css
/* API-DEMO page/component/canvas/canvas.acss */
.canvas-view {
  display: flex;
  justify-content: center;
}
.canvas {
  width: 305px;
  height: 305px;
  background-color: #fff;
}
```

### Bug & Tip 

- 使用新的 canvas 接口必须指定 type 类型。
- 通过 [SelectorQuery](https://opendocs.alipay.com/mini/api/pc8s51) 接口获取 canvas 实例，最好在 canvas 组件的 onReady 回调函数中调用。
- 基于以上 2 点，可通过 my.canIUse('canvas.type') & my.canIUse('createSelectorQuery.return.node')来做可用性检测。

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| id | String | 组件唯一标识符。<br />**注意**：同一页面中的 id 不可重复。 |
| style | String | - |
| class | String | - |
| width | String | **默认值：** 300px |
| height | String | **默认值：** 225px |
| disable-scroll | Boolean | 禁止屏幕滚动以及下拉刷新。<br />**默认值：** false |
| onTap | EventHandle | 点击。 |
| onTouchStart | EventHandle | 触摸动作开始。 |
| onTouchMove | EventHandle | 触摸后移动。 |
| onTouchEnd | EventHandle | 触摸动作结束。 |
| onTouchCancel | EventHandle | 触摸动作被打断，如来电提醒，弹窗。 |
| onLongTap | EventHandle | 长按 500ms 之后触发，触发了长按事件后进行移动将不会触发屏幕的滚动。 |
| type | String | 类型。设置 type 属性后，会渲染成 native canvas。<br />**可选值**：2d、webgl<br />**版本要求**：基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onReady | EventHandle | canvas 组件初始化成功触发。<br />**版本要求**：基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |

**注意：** 如果需要在高 DPR（devicePixelRatio）下取得更细腻的显示，需要先将 [canvas](https://opendocs.alipay.com/mini/component/canvas#%E5%8E%9F%E7%94%9F%20Canvas%20%E7%BB%84%E4%BB%B6%E9%80%82%E9%85%8D) 用属性设置放大，用样式缩小，例如：
```html
<!-- getSystemInfoSync().pixelRatio === 2 -->
<canvas width="200" height="200" style="width:100px;height:100px;"/>
```

# 附录：原生 Canvas 组件适配

## 简介
为了提升性能、优化小程序体验，canvas 组件会逐步切换为原生 canvas 组件实现。实际使用中若遇到 iOS 平台上覆盖于 canvas 组件上的 web 元素（后称：覆盖元素）无法收到 UI 事件时，可以进行如下适配，以确保顺利收到 UI 事件。

#### 使用限制

- 基础库版本 2.6.2 及以上。
- 支付宝版本 10.2.0 及以上。

## 使用
以下两个步骤缺一不可：

1. 当前小程序 app.json 的 `window` 节点中配置 `enableComponentOverlayer` 为 "YES"。
```javascript
{
	  "pages":[
		  "pages/index/index"
	  ],
	  "window":{
		  "enableComponentOverlayer":"YES"
	  }
  }
```

2. 这个配置项用于指示小程序运行时将目标区域内 UI 事件派发给 canvas 组件。
2. 为覆盖元素添加 `AF-COMPONENT-OVERLAYER` class 属性来指示小程序运行时将 UI 事件派发给覆盖元素，而不传递给后边的 Canvas 组件；若不添加 `AF-COMPONENT-OVERLAYER` class 属性，则会默认派发给 canvas 组件。
```css
/* declare style for top class in acss */
.top {
  z-index: 2;
}
```


```css
<!-- axml 中为覆盖元素增加 AF-COMPONENT-OVERLAYER class 属性的样例 -->
<view class="page">
  <canvas style="width: 100%; height: 500px;"></canvas>
  <!-- 假设下面的View需要盖在 canvas 上（即 z-index 层级要比 canvas 高），那么需要在这个 view 上增加class "AF-COMPONENT-OVERLAYER" 这样-->
    <view class="top AF-COMPONENT-OVERLAYER" onTap="viewClick"  >
    </view>
</view>
```
**注意：** 如果在开发中遇到 canvas 组件上没有可见的 web 元素覆盖（即：开发视角下无覆盖元素）时也收不到 UI 事件，可以只采用步骤 1 来尝试解决。 

