
# 简介
开始监听帧数据。

## 使用限制

- 基础库 [1.18.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
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
    // 开始监听帧数据
    listener.start();
    
    // 20秒后停止监听帧数据
    setTimeout(() => {
    	listener.stop();
    }, 20000);
  },
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

