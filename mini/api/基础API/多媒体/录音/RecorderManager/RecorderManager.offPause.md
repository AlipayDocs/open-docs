# 简介
取消监听录音暂停事件。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let recorderManager = my.getRecorderManager();
const recorderPauseCallback = res => {
 console.log('暂停录音');
};
recorderManager.onPause(recorderPauseCallback);
recorderManager.start();
setTimeout(() => {
 // 2秒后暂停录音
  recorderManager.pause();
}, 2000);
setTimeout(() => {
  // 3秒后移除监听录音暂停事件
 recorderManager.offPause(recorderPauseCallback);
}, 3000);
```

## 入参

### Function callback
录音暂停事件的回调函数。
