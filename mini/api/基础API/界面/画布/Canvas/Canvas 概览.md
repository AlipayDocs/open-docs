Canvas 实例，可以通过 [SelectorQuery](https://opendocs.alipay.com/mini/api/pc8s51) 获取。

## 使用限制

- **基础库** [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 由于 iOS 真机在 10.2.28 有 bug，若需使用 Canvas 新接口，短期内需要联系技术支持进行处理（点击右侧咨询按钮接入）。

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
