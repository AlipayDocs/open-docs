
# 简介
**my.offError** 是取消监听小程序错误事件的 API。

## 使用限制

- 基础库 [1.21.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
App({
  onShow() {
    this.handleError = error => {
      // 小程序执行出错时
      console.log(error);
    }
    // 注意，error 的类型为 String
    my.onError(this.handleError);
  },
  onHide() {
    // 取消监听 error 事件
    my.offError(this.handleError);
  }
})
```

## 入参
入参为回调函数：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| 回调函数 | Function | 小程序 JS 错误事件的回调函数。 |

