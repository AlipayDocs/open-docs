# 简介

暂停录音。

## 使用限制

- 支付宝客户端 10.1.60、基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请以真机调试结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
let recorderManager = my.getRecorderManager();
recorderManager.start({
  duration: 180000,
});
recorderManager.pause();
```
