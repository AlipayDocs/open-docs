# 简介

继续录音，即恢复之前暂停的录音。

## 使用限制

- 支付宝客户端  10.1.60，基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
let recorderManager = my.getRecorderManager();
recorderManager.onPause(res => {
  console.log('暂停录音');
});
recorderManager.onResume(res => {
  console.log('继续录音');
});
recorderManager.start({
  duration: 600000,
});
recorderManager.pause();
setTimeout(() => {
  recorderManager.resume();
}, 5000);
```
