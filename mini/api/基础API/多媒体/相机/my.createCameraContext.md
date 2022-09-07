# 简介

创建 [camera](https://opendocs.alipay.com/mini/03qegu) 上下文 [CameraContext](https://opendocs.alipay.com/mini/03qcav) 对象。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 需在组件初始化完成后即 `onReady` 回调触发后执行 `my.createCameraContext`。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

## 示例代码

### .axml 示例代码

```html
<camera 
  id="camera"
  device-position="front"
  flash="off"
  style="width: 100%; height: 300px;"
  onReady="onCameraReady"
/>
```

### .js 示例代码

```javascript
Page({
  onCameraReady(e) {
    console.log('相机初始化完成');
    this.cameraContext = my.createCameraContext('camera');
  },
})
```

### 返回值

[CameraContext](https://opendocs.alipay.com/mini/03qcav) camera 上下文。
