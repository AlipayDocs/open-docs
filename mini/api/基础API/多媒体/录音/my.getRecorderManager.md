# 简介
获取 **全局唯一** 的录音管理器 RecorderManager。如何接入以及更多介绍信息请参见 [RecorderManager 概览](https://opendocs.alipay.com/mini/api/recordermanager)。

## 使用限制

- 支付宝客户端 10.1.60，**基础库** [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let recorderManager = my.getRecorderManager();
```

## 返回值
[RecorderManager](https://opendocs.alipay.com/mini/api/recordermanager) 录音管理器。
