# 简介

**my.onUnhandledRejection** 是监听未处理的 `Promise` 拒绝事件（即 `unhandledrejection` 事件）的 API。当 `Promise` 被 `reject` 且没有 reject 处理器的时候，会触发 `unhandledrejection` 事件，该事件的回调时机和参数与 [App.onUnhandledRejection](https://opendocs.alipay.com/mini/framework/app-detail) 的一致。

## 使用限制

- 基础库 [1.24.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 如果 [app.onUnhandledRejection](<https://opendocs.alipay.com/mini/framework/app-detail#onUnhandledRejection(object%3A%20Object)>) 方法 或 my.onUnhandledRejection(callback) 的回调函数内继续触发 `Promise` 的 `unhandledrejection` 事件，则可能会导致循环触发 `unhandledrejection` 事件，请注意规避。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
App({
  onShow(options) {
    my.onUnhandledRejection(res => {
      console.log(res.reason);
      console.log(res.promise);
    });
  },
});
```

## 入参

入参为回调函数：

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| 回调函数 | Function | 当 `Promise` 被 `reject` 且没有 `reject` 处理器的时候，会触发 `unhandledrejection` 事件。 |

### 回调函数

回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **说明**                      |
| -------- | -------- | ----------------------------- |
| reason   | String   | 拒绝原因，一般是 error 对象。 |
| promise  | Promise  | 被拒绝的 Promise 对象。 </br> 注： Android 不支持返回此字段。     |
