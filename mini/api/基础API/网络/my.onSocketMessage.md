
# 简介
**my.onSocketMessage** 是监听 WebSocket 接受到服务器的消息事件的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
**注意**：案例仅供参考，建议使用自己的地址进行测试。
```javascript
// .js
my.connectSocket({
  url: '服务器地址'
})
my.onSocketMessage(function(res) {
  console.log('收到服务器内容：' + res.data)
})
```

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | String / ArrayBuffer | 服务器返回的消息：普通的文本 String 或者经 base64 编码后的 String。 |
| isBuffer | Boolean | 如果此字段值为`true`，`data`字段表示接收到的经过了 base64 编码后的 String，否则 `data` 字段表示接收到的普通 String 文本。 |

