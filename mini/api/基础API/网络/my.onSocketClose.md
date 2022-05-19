
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
    my.onSocketClose((res) => {
      my.alert({ content: "连接已关闭！" });
      this.setData({
        sendMessageAbility: false,
        closeLinkAbility: false,
      });
    });
    // 注意： 回调方法的注册在整个小程序启动阶段只要做一次，调多次会有多次回调
    my.onSocketOpen(() => {
      my.alert({ content: "连接已打开！" });
      this.setData({
        sendMessageAbility: true,
        closeLinkAbility: true,
      });
    });
    my.onSocketError(function (res) {
      my.alert({
        content: "WebSocket 连接打开失败，请检查！" + res,
      });
    });
    // 注意： 回调方法的注册在整个小程序启动阶段只要做一次，调多次会有多次回调
    my.onSocketMessage((res) => {
      my.alert({ content: "收到数据！" + JSON.stringify(res) });
    });
  },
  connect_start() {
    my.connectSocket({
      url: "服务器地址", // 开发者服务器接口地址，必须是 wss 协议，且域名必须是后台配置的合法域名
      success: (res) => {
        my.showToast({
          content: "success", // 文字内容
        });
      },
      fail: () => {
        my.showToast({
          content: "fail", // 文字内容
        });
      },
    });
  },
});
```

## 入参
Obejct 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| callback | Function | 是 | WebSocket 连接关闭事件的回调函数。 |
