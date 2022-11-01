小程序的旧版 [CanvasContext](https://opendocs.alipay.com/mini/api/canvascontext) 相关 API 已经不再维护，本指南主要介绍迁移至新版 [Canvas 2D](https://opendocs.alipay.com/mini/01vzqv) 的操作方法。<br />新版本 Canvas API 对齐 Web 标准，可以直接参考 [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)。

## 特性差异
| **功能** | **旧版** | **新版** |
| --- | --- | --- |
| API 支持 | 部分支持 Web 标准 | 支持全部 Web 标准 |
| 绘制 | 异步绘制 | 同步绘制 |
| webgl | 不支持 | 支持 WebGL 1.0 定义的属性和方法 |


## 迁移步骤

### 修改 AXML
新版 API 的 type 为必填属性。
```html
<!-- 旧版 -->
<canvas id="my-canvas" />
<!-- 改为如下新版。必须在 onReady 回调中获取 CanvasContext -->
<canvas id="my-canvas" type="2d" onReady="onCanvasReady" />
```

### 修改 CanvasContext 获取方法
旧版 canvas 接口使用 my.createCanvasContext 同步获取 CanvasContext。<br />新版 Canvas 2D 接口需要先通过 SelectorQuery 获取 Canvas 对象，再通过 Canvas.getContext 获取渲染上下文 RenderingContext。
```javascript
// 旧版
Page({
    onLoad() {
        const context = my.createCanvasContext('my-canvas');
    }
})
// 改为如下新版
Page({
    onCanvasReady() {
        my.createSelectorQuery()
            .select('#my-canvas')
            .node()
            .exec((res) => {
                const canvas = res[0].node;
                const context = canvas.getContext('2d');
            });
    },
});
```

### 修改绘制方法
旧版 canvas 接口绘制需要调用 [CanvasContext.draw](https://opendocs.alipay.com/mini/api/he6iwx) 后才会进行绘制，并且绘制过程是 **异步** 的，需要等待绘制完成回调才能进行下一步操作。<br />新版 Canvas 2D 接口不再需要调用 draw 函数，所有绘制方法都会 **同步** 绘制到画布上。<br />**注意：**CanvasContext.draw 函数第一个参数控制在绘制前是否保留上一次绘制（默认值为 false）。若在旧接口中设置为 false，则迁移至新接口后，需要在绘制前通过 [clearRect](https://opendocs.alipay.com/mini/api/xg3h06) 清空画布。
```javascript
// 旧版
// 若干绘制调用
context.fillRect(0, 0, 50, 50)
context.draw(false, () => {
    // 此时绘制完成
    console.log('draw done')
})
// 改为如下新版
// 绘制前清空画布
context.clearRect(0, 0, canvas.width, canvas.height)
// 若干绘制调用
context.fillRect(0, 0, 50, 50)
// 此时绘制完成
console.log('draw done')
```

### 修改图片绘制
旧版 canvas 接口 CanvasContext.drawImage 直接传入图片 URL。<br />新版 Canvas 2D 接口需要先通过 Canvas.createImage 创建图片对象，onload 图片加载完成回调触发后，再将图片对象传入 context.drawImage 进行绘制。
```javascript
// 旧版
const src = 'https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg'
context.drawImage(src, 2, 2, 250, 80);
// 改为如下新版
const img = canvas.createImage();
img.src = "https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg";
img.onload = () => {
  context.drawImage(img, 10, 10, 100, 100);
}
```

### 修改 toTempFilePath
```javascript
// 旧版
context.toTempFilePath({
  success(res) {
    console.log(res.apFilePath);
  },
});
// 修改为如下新版
my.canvasToTempFilePath({
    canvas,
    success(res) {
      console.log('success', res.tempFilePath);
    }
});
```
