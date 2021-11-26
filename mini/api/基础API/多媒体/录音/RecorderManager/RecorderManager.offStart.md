
# 简介
取消监听录音开始事件。

## 使用限制

- **基础库** [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let recorderManager = my.getRecorderManager();
const recorderStartCallback = res => {
 console.log('开始录音');
};
recorderManager.onStart(recorderStartCallback);
setTimeput(() => {
 recorderManager.offStart(recorderStartCallback);
}, 5000);
```

## 入参

### function callback
录音开始事件的回调函数。
