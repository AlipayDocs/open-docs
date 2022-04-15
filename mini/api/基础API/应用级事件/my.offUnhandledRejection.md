# 简介
**my.offUnhandledRejection** 是取消监听 `unhandledrejection` 事件的 API。

## 使用限制
- 基础库 [1.24.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用
## 示例代码
### .js 示例代码
```javascript
//.js
App({
  onShow(options) {
    const handleRejection = (res) => {
      console.log(res.reason);
      console.log(res.promise);
    }
    my.onUnhandledRejection(handleRejection);
    my.offUnhandledRejection(handleRejection);
  }
})
```

## 入参
入参为回调函数：
| **参数** | **类型** | **描述** |
| --- | --- | --- |
| 回调函数 | Function | 当 `Promise` 被 `reject` 且没有 `reject` 处理器的时候，会触发 `unhandledrejection` 事件。 |
