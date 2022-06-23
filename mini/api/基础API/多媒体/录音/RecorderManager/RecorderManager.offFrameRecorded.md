# 简介
取消监听已录制完制定帧大小的文件事件。如果设置了 frameSize，则会回调此事件。

## 使用限制

- 支付宝 10.1.80，基础库 [1.12.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- iOS 只支持 iOS11 以上系统。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let recorderManager = my.getRecorderManager();
const frameRecordedCallback = res => {
 console.log(res.frameBuffer, res.isLastFrame);
}
recorderManager.onFrameRecorded(frameRecordedCallback)
recorderManager.start({
  frameSize: 100,
})
setTimeout(() => {
 recorderManager.offFrameRecorded(frameRecordedCallback)
}, 50000)
```

## 入参

### Function callback
已录制完指定帧大小的文件事件的回调函数。
