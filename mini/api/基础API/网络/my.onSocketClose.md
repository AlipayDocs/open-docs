# 简介

**my.onSocketClose** 是监听 WebSocket 关闭事件的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

案例仅供参考，建议使用自己的地址进行测试。

```javascript
// .js
Page({
  onLoad() {
    // 注意： 回调方法的注册在整个小程序启动阶段只要做一次，调多次会有多次回调
    my.onSocketClose(res => {
      console.log('onSocketClose 连接关闭！');
    });
  },
  connect_socket() {
    my.connectSocket({
      url: 'wss://...', // 开发者服务器接口地址，必须是 wss 协议
    });
  },
  close_socket() {
    // 通过 onSocketClose 监听关闭成功事件
    my.closeSocket({
      success: (res) => {
        console.log("closeSocket 关闭成功!");
      },
    })
  },
});
```

## 入参

Obejct 类型，属性如下：

| **属性** | **类型** | **必填** | **描述**                           |
| -------- | -------- | -------- | ---------------------------------- |
| callback | Function | 是       | WebSocket 连接关闭事件的回调函数。 |
