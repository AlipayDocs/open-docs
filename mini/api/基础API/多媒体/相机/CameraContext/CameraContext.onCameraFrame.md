
# 简介
**CameraContext.onCameraFrame** 获取 Camera 实时帧数据。

## 使用限制

- 基础库 [1.18.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 使用该接口需同时在 [camera](https://opendocs.alipay.com/mini/03qegu) 组件属性中指定 `frame-size`（默认值为 `medium`）。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .axml 示例代码<br />
```html
<camera 
  id="camera"
  device-position="front"
  flash="off"
  style="width: 100%; height: 300px;"
  frame-size="medium"
  onReady="onCameraReady"
/>
```

### .js 示例代码
```javascript
Page({
  onCameraReady(e) {
    console.log('相机初始化完成');
    this.cameraContext = my.createCameraContext('camera');
    const listener = this.cameraContext.onCameraFrame((frame) => {
      console.log(frame.data instanceof ArrayBuffer, frame.width, frame.height);
    })
    listener.start();
  },
})
```

## 入参

### Function callback
回调函数。

#### 属性
callback 函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| width | Number | 图像数据矩形的宽度。 |
| height | Number | 图像数据矩形的高度。 |
| data | ArrayBuffer | 图像像素点数据，一维数组，每四项表示一个像素点的 rgba。 |


## 返回值
[CameraFrameListener](https://opendocs.alipay.com/mini/03qgue)
