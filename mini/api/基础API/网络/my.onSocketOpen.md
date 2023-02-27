# 简介

**my.onSocketOpen** 是监听 WebSocket 连接打开事件的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

案例仅供参考，建议使用自己的地址进行测试。

```javascript
// .js
my.connectSocket({
  url: 'wss://...', // 开发者服务器接口地址，必须是 wss 协议
});
my.onSocketOpen(function () {
  console.log('WebSocket 连接已打开！');
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述**                           |
| -------- | -------- | -------- | ---------------------------------- |
| callback | Function | 是       | WebSocket 连接打开事件的回调函数。 |
