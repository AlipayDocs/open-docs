# 简介

获取全局唯一的录音管理器，可通过 [my.getRecorderManager](https://opendocs.alipay.com/mini/api/getrecordermanager) 获取。<br />录音管理器提供了开始录音、暂停、继续、停止、取消及隐藏录音图标等功能，还可以结合  **[音频播放 API](https://opendocs.alipay.com/mini/03l3fn)** 快速开发具有音频录制、音频播放功能的小程序。

## 使用限制

- 支付宝客户端 10.1.60，基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- 音频内容需健康文明，相关规定可查看 [小程序违规处理规则](https://docs.open.alipay.com/rules_mini/nowgsa)。若发布后内容涉及违规，支付宝将根据小程序服务协议、本规则及相应细则对音频、开发者以及小程序采取相应管理措施。

## 方法

| **名称** | **功能说明** |
| --- | --- |
| [RecorderManager.start](https://opendocs.alipay.com/mini/api/recordermanager/start) | 开始录音。 |
| [RecorderManager.pause](https://opendocs.alipay.com/mini/api/recordermanager/pause) | 暂停录音。 |
| [RecorderManager.resume](https://opendocs.alipay.com/mini/api/recordermanager/resume) | 继续录音，即恢复之前暂停的录音。 |
| [RecorderManager.stop](https://opendocs.alipay.com/mini/api/recordermanager/stop) | 停止录音。 |
| [RecorderManager.onStart](https://opendocs.alipay.com/mini/api/recordermanager/onstart) | 监听录音开始事件。 |
| [RecorderManager.offStart](https://opendocs.alipay.com/mini/api/recordermanager/offstart) | 取消监听录音开始事件。 |
| [RecorderManager.onPause](https://opendocs.alipay.com/mini/api/recordermanager/onpause) | 监听录音暂停事件。 |
| [RecorderManager.offPause](https://opendocs.alipay.com/mini/api/recordermanager/offpause) | 取消监听录音暂停事件。 |
| [RecorderManager.onResume](https://opendocs.alipay.com/mini/api/recordermanager/onresume) | 监听录音继续事件。 |
| [RecorderManager.offResume](https://opendocs.alipay.com/mini/api/recordermanager/offresume) | 取消监听录音继续事件。 |
| [RecorderManager.onStop](https://opendocs.alipay.com/mini/api/recordermanager/onstop) | 监听录音结束事件。 |
| [RecorderManager.offStop](https://opendocs.alipay.com/mini/api/recordermanager/offstop) | 取消监听录音结束事件。 |
| [RecorderManager.onError](https://opendocs.alipay.com/mini/api/recordermanager/onerror) | 监听录音错误事件。 |
| [RecorderManager.offError](https://opendocs.alipay.com/mini/api/recordermanager/offerror) | 取消监听录音错误事件。 |
| [RecorderManager.onFrameRecorded](https://opendocs.alipay.com/mini/api/recordermanager/onframerecorded) | 监听已录制完制定帧大小的文件事件。如果设置了 frameSize，则会回调此事件。 |
| [RecorderManager.offFrameRecorded](https://opendocs.alipay.com/mini/api/recordermanager/offframerecorded) | 取消监听已录制完制定帧大小的文件事件。 |
| [RecorderManager.onDecibelChange](https://opendocs.alipay.com/mini/01acgm) | 监听声音的分贝变化事件。 |
| [RecorderManager.offDecibelChange](https://opendocs.alipay.com/mini/03hbnp) | 取消监听声音分贝变化事件。 |


## 如何播放录音文件

可使用 **[音频播放 API](https://opendocs.alipay.com/mini/03l3fn)**，将 onStop 返回值中 tempFilePath（文件临时路径）作为音频源 src 播放录制音频。以前景音频播放为例（录制音频等操作请查看前文完成）：

```javascript
const innerAudioContext = my.createInnerAudioContext();
const recorderManager = my.getRecorderManager();

// 监听播放录音事件
innerAudioContext.onPlay = function () {
  console.log('onPlay');
  my.alert({ content: 'onPlay' });
};
// 监听录音停止事件，获取录音文件地址
recorderManager.onStop(res => {
  console.log('recorder onStop', JSON.stringify(res));
  my.alert({
    content:
      'recorder onStop' + JSON.stringify(res) + '  ' + res.tempFilePath,
  });

  // 将文件临时路径 tempFilePath 作为音频播放源
  innerAudioContext.src = res.tempFilePath;
  //backgroundAudioManager.src = res['tempFilePath'];
});

Page({
  playAudio() {
    my.alert({ content: innerAudioContext.src + '-----' });
    innerAudioContext.play();
  },
});
```

# 快速示例

支付宝还提供了简单的快速示例，方便开发者快速上手使用录音功能。点此下载 [快速示例](https://gw.alipayobjects.com/os/bmw-prod/6983def6-6052-4479-a37a-bbff8ca6c6ae.zip)。
