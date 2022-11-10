
# 简介
**CameraContext.startRecord** 开始录像。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
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
// camera.js
Page({
  onCameraReady(e) {
    console.log('相机初始化完成');
    this.cameraContext = my.createCameraContext('camera');
    let count = 0;
    setInterval(() => {
      count++;
    }, 1000);
    this.cameraContext.startRecord({
      timeoutCallback(res) {
        console.log('超时结束录制');
        console.log('累计时间为' + count);
      },
      timeout: 10
    });
  },
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| timeoutCallback | Function | 否 | 录像超过 30s 或页面 `onHide` 时会结束录像。 |
| timeout | Number | 否 | 录制时长上限，单位为秒，默认 30s ，最大录制时长 10 分钟。<br/> 基础库 2.8.2 开始支持。|
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### Function timeoutCallback
timeoutCallback 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| tempThumbPath | String | 封面图片文件地址（[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)）。 |
| tempVideoPath | String | 视频文件地址（[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)）。 |
| height | String | 视频文件的高度。<br>基础库 2.8.0 开始支持。 |
| width | String | 视频文件的宽度。<br>基础库 2.8.0 开始支持。 |
| size | String | 视频文件的尺寸。<br>基础库 2.8.0 开始支持。 |
| duration | String | 录制的持续时间。<br>基础库 2.8.0 开始支持。 |
