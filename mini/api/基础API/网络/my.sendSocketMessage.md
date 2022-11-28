# 简介

**my.sendSocketMessage** 通过 WebSocket 连接发送数据。

需要先使用 [my.connectSocket](/mini/api/vx19c3) 建立连接，在 [my.onSocketOpen](/mini/api/itm5og) 回调之后再发送数据。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
my.sendSocketMessage({
  data: this.data.toSendMessage, // 需要发送的内容
  success: res => {
    my.alert({ content: '数据发送！' + this.data.toSendMessage });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| data | String | 是 | 需要发送的内容：普通的文本内容 String 或者经 Base64 编码后的 String。 |
| isBuffer | Boolean | 否 | <li>如果发送二进制数据，需要将入参数据经 Base64 编码成 String 后赋值 `data`，同时将此字段设置为 true。</li><li>如果是普通的文本内容 String，则不需要设置此字段。</li> |
| success | Function | 否 | 回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 1 | 未知错误。 | - |
| 10 | 网络连接没有打开，无法发送消息。 | 请正常连接服务器后再调用 my.sendSocketMessage 发送数据消息。可通过 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 监听事件来判断与服务器建立正确连接。 |
