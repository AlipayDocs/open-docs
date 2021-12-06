基础库版本 1.10.0 开始支持，低版本需要做兼容处理<br />相机组件。

## 示例代码
```html
<!-- camera.axml -->
<view class="page-body">
  <view class="page-body-wrapper">
    <camera id="camera11" device-position="front" onError="error" onStop="stop" flash="off"  style="width: 100%; height: 300px;"></camera>
    <view class="btn-area">
      <button type="primary" onTap="takePhoto">拍照</button>
    </view>
    <picker onChange="chooseRecordQuanlity"  value="{{recordQualityIndex}}" range="{{recordQualityArr}}" >
        <view class="row">
          <view class="row-title">拍照质量</view>
          <view class="row-extra">当前选择：{{recordQuality}}</view>
        </view>
    </picker>
    <view class="btn-area">
      <button type="primary" onTap="startRecord">开始录像</button>
    </view>
    <view class="btn-area">
      <button type="primary" onTap="stopRecord">结束录像</button>
    </view>
    <view class="preview-tips">预览</view>
    <image a:if="{{url}}" mode="widthFix" src="{{url}}"></image>
     <video 
      src="{{videoSrc}}"
      poster="{{poster}}" 
      class="video" 
      id="video"
      enableNative="{{true}}"
      >
    </video>
  </view>
</view>
```


```javascript
// camera.js
Page({
  data: {
    url:'',
    videoSrc:'',
    poster:'',
    recordQualityArr : ["high", 'normal', 'low', 'default'],
    recordQualityIndex : 0,
    recordQuality: 'default'
  },
  onLoad() {
    this.ctx = my.createCameraContext("camera11");
  },
  takePhoto() {
    this.ctx.takePhoto({
      quality : this.data.recordQuality,
      success: (res) => {
        console.log('takePhoto success' + JSON.stringify(res))
        this.setData({
          url: res.tempImagePath,
        })
      },
      fail: (res) => {
        console.log(res);
        my.alert({ content: 'takePhoto fail' + JSON.stringify(res) });
      },
      complete: (res) => {
        console.log(res);
        my.alert({ content: 'takePhoto complete' + JSON.stringify(res) });
      },
    })
  },
  startRecord() {
    this.ctx.startRecord({
      success: (res) => {
        console.log('startRecord success' + JSON.stringify(res))
      },
      fail :(res) => {
        console.log('startRecord fail' + JSON.stringify(res) )
      },
      complete: (res) => {
        console.log('startRecord complete' + JSON.stringify(res))
      },
      timeoutCallback: (res) => {
        this.setData({
          poster: res.tempThumbPath, //设置video组件poster
          videoSrc: res.tempVideoPath //设置video组件src
        })
        console.log('startRecord timeoutCallback' + + JSON.stringify(res) )
      }
    })
  },
  stopRecord() {
    this.ctx.stopRecord({
      success: (res) => {
        this.setData({
          poster: res.tempThumbPath, //设置video组件poster
          videoSrc: res.tempVideoPath //设置video组件src
        })
      },
      fail :(res) => {
        console.log('stopRecord fail' + JSON.stringify(res) )
      },
      complete: (res) => {
        console.log('stopRecord complete' + JSON.stringify(res))
      },
    })
  },
  error(e) {
    console.log(e.detail);
    my.alert({content : "binderror" + JSON.stringify(e)});
  },
  stop(e) {
    console.log(e.detail);
    my.alert({content : "bindstop" + JSON.stringify(e)});
  },
  chooseRecordQuanlity(e) {
      const index = e.detail.value
      const {recordQualityArr} = this.data;
      var quality = recordQualityArr[index];
      this.data.recordQuality = quality;
  }
})
```

## 属性
| **属性** | **类型** | **默认值** | **描述** | **最低版本** |
| --- | --- | --- | --- | --- |
| mode | String | normal | 应用模式。<br />合法值：<br />normal：相机模式；<br />scanCode：扫码模式。 | 1.19.0 |
| device-position | Srting | back | 摄像头选择。<br />合法值：<br />front：前置摄像头；<br />back：后置摄像头。 | - |
| flash | String | auto | 闪光灯开关。<br />合法值：<br />auto：自动； <br />on：打开；<br />off：关闭。 | 1.18.0 |
| outputDimension | String | 720P | 相机拍照、录制的分辨率有效值为 360P、540P、720P、1080P。 | 1.23.0 |
| applyMicPermissionWhenInit | Bool | true | 初始化时，是否请求麦克风权限。有效值为：true，false。 | 1.20.0 |
| frame-size | String | medium | 指定期望的相机帧数据尺寸。<br />合法值：<br />large：大尺寸帧数据（720 x 1280）；<br />medium：中尺寸帧数据（540 x 960）；<br />small：小尺寸帧数据（360 x 640）。 | 1.19.0 |
| frame-format | String | rgba | 指定期望的相机帧数据类型。<br />合法值：<br />rgba：二进制数据；<br />jpg：base64string。 | 1.21.0 |
| max-duration | Number | 30 | 允许录制的最大时长（超时自动结束）. | 10.1.98 |
| onStop | EventHandle | - | 摄像头在非正常终止时触发，如退出后台等情况。 | - |
| onError | EventHandle | - | 用户不允许使用摄像头时触发。 | - |
| onScanCode | EventHandle | - | 在扫码识别成功时触发，仅在 `mode="scanCode"` 时生效。 | 1.19.0 |


### onScanCode(Object object)
扫码识别结果

#### 参数
Object object

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| detail | map | 否 | 识别结果 |

detail 值

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| type | String | 否 | 码类型 |
| result | String | 否 | 识别结果 |



