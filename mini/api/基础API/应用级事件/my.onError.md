# 简介

**my.onError** 是监听小程序错误事件的 API。目前仅指 JS 执行错误。触发时机和参数与 [App.onError](https://opendocs.alipay.com/mini/framework/app-detail#onError(error%2C%20stack)) 一致。

## 使用限制

- 基础库 [1.21.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 使用 my.onError 监听到的报错，app.js 中的 onError 方法也会监听到。
- 使用 my.onError 监听页面报错，如果在多个页面开启监听没有关闭，则页面报错时会触发多个监听事件，建议在页面关闭时调用 [my.offError](https://opendocs.alipay.com/mini/00njqm) 关闭监听。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
App({
  onLaunch() {
    // 注意，error的类型为String
    my.onError(function(error, stack) {
      // 小程序执行出错时
      console.error(error);
      // 基础库 2.7.4 开始支持返回stack
      console.error(stack);
    });
  }
})
```

## 入参

入参为回调函数：

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| 回调函数 | Function | 小程序 JS 错误事件的回调函数。 |

### 回调函数
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| error | String | 异常描述，一般为 `Error` 对象的 `message` 字段。 |
| stack | String | 异常堆栈，一般为 `Error` 对象的 `stack` 字段。<br />基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。 |

