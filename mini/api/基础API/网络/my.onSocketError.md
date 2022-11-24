# 简介

**my.onSocketError** 是监听 WebSocket 错误事件的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

案例仅供参考，建议使用自己的地址进行测试。

```javascript
// .js
my.connectSocket({
  url: '开发者的服务器地址',
});
my.onSocketOpen(function () {
  console.log('WebSocket 连接已打开！');
});
my.onSocketError(function (res) {
  console.log('WebSocket 连接打开失败，请检查！');
});
```

## 入参

Obejct 类型，属性如下：

| **属性** | **类型** | **必填** | **描述**                       |
| -------- | -------- | -------- | ------------------------------ |
| callback | Function | 是       | WebSocket 错误事件的回调函数。 |

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 1 | Error Unknown。 | 未知错误 |
| 8 | Invalid Sec-WebSocket-Accept response. | 请指定 Sec-WebSocket-Protocol 请求头。 |
| 50 | unknown error | 请检查网络连接。 |
| 65 | unknown error | 请检查域名是否合法。 |
