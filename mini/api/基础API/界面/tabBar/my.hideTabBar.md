# 简介
**my.hideTabBar** 是隐藏 tabBar 的 API。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.hideTabBar({
  animation: true,
  success: (res) => console.log('hideTabBar success'),
  fail: (res) => my.alert({ title: 'hideTabBar failed', content: JSON.stringify(res) }),
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| animation | Boolean | 否 | 是否需要动画效果，默认为无动画效果。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码
fail 回调会收到一个 Object 类型的参数，其 error 属性为错误码，errorMessage 为错误消息。

| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 11 | 当前页面不在 tabBar 上。  | 报错原因为 app.json 中未配置 tabBar。请在配置以后再在 tabBar 页面中调用本接口。 |


# Bug & Tip

* `Bug` app.json 里已配置 tabBar 的情况下，在通过 my.nativeTo/my.redirectTo 到达的页面里，调用此 API 无回调。

更多 tabBar 相关问题可查看 [tabBar 常见问题](https://opendocs.alipay.com/mini/api/do7urq)。
