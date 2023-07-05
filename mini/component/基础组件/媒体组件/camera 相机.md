# 简介
系统相机。<br />相关 API：[my.createCameraContext](https://opendocs.alipay.com/mini/03qfj7)

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 需在组件初始化完成后即 `onReady` 回调触发后再执行 my.createCameraContext。

# 使用

## 示例代码

### .axml 示例代码
```html
<camera 
 id="camera"
  device-position="front"
 flash="off"
  style="width: 100%; height: 300px;"
  onReady="onCameraReady"
  onError="onCameraError"
  onStop="onCameraStop"
/>
```

### .js 示例代码
```javascript
Page({
  onCameraReady(e) {
   console.log('相机初始化完成');
    this.cameraContext = my.createCameraContext('camera');
    this.cameraContext.takePhoto({
     success(res) {
       console.log(res);
      }
    })
  },
  onCameraError(e) {
    console.log('相机发生异常');
  },
  onCameraStop(e) {
    console.log('相机终止');
  },
})
```

## 属性说明
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| mode | String | 应用模式。<br />**默认值：**normal<br />**版本要求**：基础库 [1.19.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。 |
| device-position	 | String | 摄像头朝向，前置或后置。可选值为 front、back。 |
| flash | String | 闪光灯。可选值为 auto、on、off。<br />**默认值：**auto<br />**版本要求**：基础库 [1.18.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。 |
| output-dimension | String | 相机拍照，录制的分辨率。<br />有效值为 360P、540P、720P、1080P、max。<br />**默认值：**720P<br />**版本要求**：基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。 |
| frame-size | String | 指定期望的相机帧数据尺寸。<br />**默认值：**medium<br />**版本要求**：基础库 [1.19.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。 |
| onReady | EventHandle | 相机初始化成功时触发。`event.detail = {maxZoom}`<br />**版本要求**：基础库 [1.24.3](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。<br />基础库 [2.7.16](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)、客户端 10.2.58 开始支持返回 `maxZoom`。 |
| onStop | EventHandle | 摄像头在非正常终止时触发，如页面隐藏、退出小程序、压后台等情况。 |
| onError | EventHandle | 用户不允许使用摄像头时触发。`event.detail = { errorCode, errorMessage }`。 |
| onScanCode | EventHandle | 在扫码识别成功时触发，仅在 mode="scanCode" 时生效。`event.detail = { type, result }`。`type` 为码类型，`result` 为识别结果。<br />**版本要求**：基础库 [1.19.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。 |


### mode 的合法值
| **值** | **说明** |
| --- | --- |
| normal | 相机模式 |
| scanCode | 扫码模式 |


### device-position 的合法值
| **值** | **说明** |
| --- | --- |
| front | 前置 |
| back | 后置 |


### flash 的合法值
| **值** | **说明** |
| --- | --- |
| auto | 自动 |
| on | 打开 |
| off | 关闭 |


### frame-size 的合法值
| **值** | **说明** |
| --- | --- |
| small | 小尺寸帧数据 (360 x 640) |
| medium | 中尺寸帧数据 (540 x 960) |
| large | 大尺寸帧数据 (720 x 1280) |


### 错误码
| **错误码** | **错误描述** |
| --- | --- |
| 1001 | 权限校验失败 |
| 1002 | 磁盘文件相关错误 |
| 1004 | 无摄像头权限 |
| 1005 | 无麦克风权限 |
| 1009 | 扫码时禁止拍照录像 |
| 1000 | 其他错误 |

