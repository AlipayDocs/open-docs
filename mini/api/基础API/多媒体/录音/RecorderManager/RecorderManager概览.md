# 简介
获取全局唯一的录音管理器，可通过 [my.getRecorderManager](https://opendocs.alipay.com/mini/api/getrecordermanager) 获取。<br />录音管理器提供了开始录音、暂停、继续、停止、取消及隐藏录音图标等功能，还可以结合 **音频播放 API** 快速开发具有音频录制、音频播放功能的小程序。

## 使用限制

- 支付宝客户端 10.1.60，基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- 音频内容需健康文明，相关规定可查看 [小程序违规处理规则](https://docs.open.alipay.com/rules_mini/nowgsa)。若发布后内容涉及违规，支付宝将根据小程序服务协议、本规则及相应细则对音频、开发者以及小程序采取相应管理措施。

## 方法
| **名称** | **功能说明** |
| --- | --- |
| [RecorderManager.start](https://opendocs.alipay.com/mini/api/recordermanager/start) | 开始录音。 |
| [RecorderManager.stop](https://opendocs.alipay.com/mini/api/recordermanager/stop) | 停止录音。 |
| [RecorderManager.pause](https://opendocs.alipay.com/mini/api/recordermanager/pause) | 暂停录音。 |
| [RecorderManager.resume](https://opendocs.alipay.com/mini/api/recordermanager/resume) | 继续录音，即恢复之前暂停的录音。 |
| [RecorderManager.onError](https://opendocs.alipay.com/mini/api/recordermanager/onerror) | 监听录音错误事件。 |
| [RecorderManager.offError](https://opendocs.alipay.com/mini/api/recordermanager/offerror) | 取消监听录音错误事件。 |
| [RecorderManager.onStart](https://opendocs.alipay.com/mini/api/recordermanager/onstart) | 监听录音开始事件。 |
| [RecorderManager.offStart](https://opendocs.alipay.com/mini/api/recordermanager/offstart) | 取消监听录音开始事件。 |
| [RecorderManager.onPause](https://opendocs.alipay.com/mini/api/recordermanager/onpause) | 监听录音暂停事件。 |
| [RecorderManager.offPause](https://opendocs.alipay.com/mini/api/recordermanager/offpause) | 取消监听录音暂停事件。 |
| [RecorderManager.onResume](https://opendocs.alipay.com/mini/api/recordermanager/onresume) | 监听录音继续事件。 |
| [RecorderManager.offResume](https://opendocs.alipay.com/mini/api/recordermanager/offresume) | 取消监听录音继续事件。 |
| [RecorderManager.onStop](https://opendocs.alipay.com/mini/api/recordermanager/onstop) | 监听录音结束事件。 |
| [RecorderManager.offStop](https://opendocs.alipay.com/mini/api/recordermanager/offstop) | 取消监听录音结束事件。 |
| [RecorderManager.onFrameRecorded](https://opendocs.alipay.com/mini/api/recordermanager/onframerecorded) | 监听已录制完制定帧大小的文件事件。如果设置了 frameSize，则会回调此事件。 |
| [RecorderManager.offFrameRecorded](https://opendocs.alipay.com/mini/api/recordermanager/offframerecorded) | 取消监听已录制完制定帧大小的文件事件。 |
| [RecorderManager.onDecibelChange](https://opendocs.alipay.com/mini/01acgm) | 监听声音的分贝变化回调事件。 |
| [RecorderManager.offDecibelChange](https://opendocs.alipay.com/mini/03hbnp) | 取消监听声音分贝变化事件。 |


# 接口调用

## 获取 recorderManager
**版本需求**：基础库 1.11.0 或更高版本；支付宝客户端 10.1.32 或更高版本。<br />可调用 [my.getRecorderManager](https://opendocs.alipay.com/mini/api/getrecordermanager) 获取全局唯一的录音管理器 recorderManager，注册监听录音开始、暂停、继续及停止事件。

### 示例代码
```javascript
let recorderManager = my.getRecorderManager();
```

## 注册监听事件
```javascript
// 监听录音开始事件
recorderManager.onStart(() => {
  console.log('recorder start')
})
// 监听录音暂停事件
recorderManager.onPause(() => {
  console.log('recorder pause')
})
// 监听录音继续事件
recorderManager.onResume(() => {
  console.log('recorder resume')
})
// 监听录音停止事件
recorderManager.onStop((res) => {
  console.log('recorder onStop', JSON.stringify(res));
  my.alert({ content: 'recorder onStop' + JSON.stringify(res) + "  " + res['tempFilePath'] });
})
// 监听录音错误事件
recorderManager.onError((res) => {
  console.log('recorder error', res)
})
// 监听已录制完制定帧大小的文件间，如果 RecorderManager.start 设置了 frameSize，则会回调此事件。
recorderManager.onFrameRecorded((res) => {
  my.alert({
    title: "onFrameRecorded",
    content: "onFrameRecorded isLastFrame" + res.isLastFrame + " frameBuffer " + res.frameBuffer.byteLength
  })
})
```
**说明：**

- recorderManager.onStop：监听录音停止事件。录音停止后将触发该事件并生成录音文件的临时路径（tempFilePath）。
- recorderManager.onFrameRecorded：监听录制完成制定帧大小的文件事件，仅当 RecorderManager.start 方法中 format 参数为 mp3 且设置了 frameSize 时回调此事件。

更多监听事件详情可查看 **方法**。

## 录音操作
可使用 recorderManager 调用方法完成开始/结束录音等操作。

### 开始录音
可调用 [RecorderManager.start](https://opendocs.alipay.com/mini/api/recordermanager/start) 开始录音。
```javascript
Start() {
   const options = {
   duration: 60000,
   sampleRate: 8000,
   numberOfChannels: 1,
   encodeBitRate: 16000,
   format: "aac",
   frameSize: null,
   audioSource: "auto",
   hideTips: false,
	}
  recorderManager.start(options)
},
```

#### 入参说明

- duration：录音时长，可选。单位毫秒（ms），默认值 60000（1 分钟），最大值 600000 ms（10 分钟）。设置该参数则录音时长达到时将自动调用 stop 方法停止录音。
- hideTips：隐藏录音图标，可选。默认 false 不隐藏。
- numberOfChannels：录音通道数，可选。默认 1，支持如下通道数量：
   - 1：1 个通道。
   - 2：2 个通道。
- format：音频格式，可选。默认 aac，支持 aac、mp3（需支付宝客户端 10.1.80 及以上版本） 格式，参数值需小写。
- frameSize：指定帧大小，可选。单位 KB，支付宝客户端 10.1.80 及以上版本支持。传入 frameSize 后，每录制指定帧大小的内容后，会回调录制的文件内容，不指定则不会回调。暂仅支持 mp3 格式设置。
- audioSource：指定录音的音频输入源，可选。可通过 my.getAvailableAudioSources()  获取当前可用的音频源。
- sampleRate：采样率，可选。默认值 8000。
   - 8000：8000 采样率。
   - 11025：11025 采样率。
   - 12000：12000 采样率。
   - 16000：16000 采样率。
   - 22050：22050 采样率。
   - 24000：24000 采样率。
   - 32000：32000 采样率。
   - 44100：44100 采样率。
   - 48000：48000 采样率。
- encodeBitRate：编码码率，可选。默认 48000。每种采样率有对应的编码码率范围有效值，设置不合法的采样率或编码码率会导致录音失败，采样率与编码码率限制如下：
| **采样率** | **编码码率** |
| --- | --- |
| 8000 | 16000 ~ 48000。 |
| 11025 | 16000 ~ 48000。 |
| 12000 | 24000 ~ 64000。 |
| 16000 | 24000 ~ 96000。 |
| 22050 | 32000 ~ 128000。 |
| 24000 | 32000 ~ 128000。 |
| 32000 | 48000 ~ 192000。 |
| 44100 | 64000 ~ 320000。 |
| 48000 | 64000 ~ 320000。 |


### 暂停录音
**版本需求**：基础库版本 1.13.0 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。<br />可调用 [RecorderManager.pause](https://opendocs.alipay.com/mini/api/recordermanager/pause) 暂停录音。
```javascript
recorderManager.pause();
```

### 继续录音
**版本需求**：基础库版本 1.13.0 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议做 **兼容处理**。<br />可调用 [RecorderManager.resume](https://opendocs.alipay.com/mini/api/recordermanager/resume) 继续录音，仅支持处于 pause 暂停状态录音继续。
```javascript
recorderManager.resume()
```

### 停止录音
**版本需求**：基础库版本 1.13.0 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议做 **兼容处理**。<br />可调用 [RecorderManager.stop](https://opendocs.alipay.com/mini/api/recordermanager/stop) 停止录音，停止录音后会触发 onStop 生成录音文件临时路径 tempFilePath。
```javascript
recorderManager.stop()
```

## 播放录音
可使用 **音频播放 API**，将 onStop 返回值中 tempFilePath（文件临时路径）作为音频源 src 播放录制音频。以前景音频播放为例（录制音频等操作请查看前文完成）：
```javascript
const innerAudioContext = my.createInnerAudioContext();
innerAudioContext.onPlay = function () {
  console.log('onPlay')
  my.alert({ content: "onPlay" });
}
// 录音停止事件中报错录音，获取录音文件地址
recorderManager.onStop((res) => {
  console.log('recorder onStop', JSON.stringify(res));
  my.alert({ content: 'recorder onStop' + JSON.stringify(res) + "  " + res['tempFilePath'] });
  // 保存本次录音文件地址
  my.saveFile({
    apFilePath: res['tempFilePath'],
    success: function (res) {
      my.alert({ content: 'recorder saveFile success' + JSON.stringify(res) });
    },
    fail: function (res) {
      my.alert({ content: 'recorder saveFile fail' + JSON.stringify(res) });
    },
    complete: function (res) {
      my.alert({ content: 'recorder saveFile complete' + JSON.stringify(res) });
    },
  })
 
  // 将文件临时路径 tempFilePath 作为音频播放源
  innerAudioContext.src = res['tempFilePath'];
  //backgroundAudioManager.src = res['tempFilePath'];
})
Page({
  playAudio() {
    my.alert({ content: innerAudioContext.src + "-----" });
    innerAudioContext.play();
  },
})
```

# 快速示例
支付宝还提供了简单的快速示例，方便开发者快速上手使用录音功能。点此下载 [快速示例](https://gw.alipayobjects.com/os/bmw-prod/6983def6-6052-4479-a37a-bbff8ca6c6ae.zip)。
