Canvas 绘图上下文。

- 通过 Canvas.getContext('2d') 接口或 OffscreenCanvas.getContext('2d') 接口，可以获取 CanvasRenderContext2D 对象，实现了 [Canvas 2D Context](https://www.w3.org/TR/2dcontext/) 定义的属性和方法。
  - CanvasRenderContext2D 提供的 API 列表：https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D
- 通过 Canvas.getContext('webgl') 接口或 OffscreenCanvas.getContext('webgl') 接口 ，可以获取 WebGLRenderingContext 对象，实现了 [WebGL 1.0](https://www.khronos.org/registry/webgl/specs/latest/1.0/) 定义的属性和方法。
  - WebGLRenderingContext 提供的 API 列表：https://developer.mozilla.org/zh-CN/docs/Web/API/WebGLRenderingContext

## 使用限制

- 基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
