# 简介

**my.closeSocket** 是关闭 [WebSocket](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket) 连接的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

注意：案例仅供参考，建议使用自己的地址进行测试。

```javascript
// .js
my.onSocketOpen(function () {
  my.closeSocket();
});
my.onSocketClose(function (res) {
  console.log('WebSocket 已关闭！');
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
