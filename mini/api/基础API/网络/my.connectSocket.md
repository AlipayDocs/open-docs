
# 简介
**my.connectSocket** 用于创建一个 [WebSocket](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket) 的连接。一个支付宝小程序在一段时间内只能保留一个 WebSocket 连接，如果当前已存在 WebSocket 连接，那么会自动关闭该连接，并重新创建一个新的 WebSocket 连接。 

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/adccc0ecd4072e1b0fccc2cacf01ec8d.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fc3f122b0dbbcef4cb9d4b17f5bb0232.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
**注意**：案例仅供参考，建议使用自己的地址进行测试。

### .js 示例代码
```javascript
// .js
my.connectSocket({
  url: this.data.websocketServer, // 开发者服务器接口地址，必须是 wss 协议，且域名必须是后台配置的合法域名
  data: {},
  header:{
    'content-type': 'application/json'
  },
  success: (res) => {
     console.log('WebSocket 连接成功');
  },
  fail: () => {
     my.showToast({
        content: 'fail', // 文字内容
     });
  }
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 目标服务器接口地址。<br />**注意：**部分新发布的小程序只支持 wss 协议。 |
| data | Object | 否 | 请求的参数。 |
| header | Object | 否 | 设置请求的头部。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 1 | 未知错误。 | - |
| 2 | 网络连接已经存在。 | 一个支付宝小程序在一段时间内只能保留一个 WebSocket 连接。如果当前已存在 WebSocket 连接，那么会自动关闭该连接，并重新创建一个新的 WebSocket 连接。 |
| 3 | URL 参数为空。 | 替换 URL 链接。 |
| 4 | 无法识别的 URL 格式。 | 替换 URL 链接。 |
| 5 | URL 必须以 ws 或者 wss 开头。 | 替换 URL 链接。 |
| 6 | 连接服务器超时。 | 稍后重试。 |
| 7 | 服务器返回的 https 证书无效。 | 小程序必须使用 HTTPS/WSS 发起网络请求。请求时系统会对服务器域名使用的 HTTPS 证书进行校验，如果校验失败，则请求不能成功发起。由于系统限制，不同平台对于证书要求的严格程度不同。为了保证小程序的兼容性，建议开发者按照最高标准进行证书配置，并使用相关工具检查现有证书，确保其符合要求。 |
| 8 | 服务端返回协议头无效。 | 从 2019 年 5 月开始新创建的小程序，默认强制使用 HTTPS 和 WSS 协议，不再支持 HTTP 和WS 协议。 |
| 9 | WebSocket 请求没有指定 Sec-WebSocket-Protocol 请求头。 | 请指定 Sec-WebSocket-Protocol 请求头。 |
| 10 | 网络连接没有打开，无法发送消息。 | 请正常连接服务器后再调用 [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1) 发送数据消息，可通过 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 监听事件来判断与服务器建立正确连接。<br />**注意**：通过 WebSocket 连接发送数据，需要先使用 [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) 发起连接，在 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 回调之后再调用 [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1) 发送数据。 |
| 11 | 消息发送失败。 | 稍后重试。 |
| 12 | 无法申请更多内存来读取网络数据。 | 请检查内存。 |


# 常见问题 FAQ

## Q：my.connectSocket是成功的，进入success，却没有进入my.onSocketOpen，反而直接进入了my.onSocketError，报错503，是什么原因？
A：检查服务端是否能够正常连接。原因是：排查客户端日志发现服务端拒绝握手，报错信息“refuse handshake”。


