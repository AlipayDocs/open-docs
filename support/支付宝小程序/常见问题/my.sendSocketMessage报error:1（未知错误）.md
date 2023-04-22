## 错误码
1

## 报错描述
my.sendSocketMessage 通过 WebSocket 连接发送数据消息报 error: 1,errorMessage:未知错误。

## 涉及接口

- [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3)
- [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1)

## 报错原因
WebSocket 连接与服务器连接异常，my.sendSocketMessage 发送数据消息报错 error:1（未知错误）。

## 解决方案

- 重新与服务器建立 WebSocket 连接，确认正常连接服务器后再 my.sendSocketMessage 发送数据消息，可通过 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 监听来判断是否正确与服务器建立连接。
- 如果是在 IDE 报错，建议进行真机调试/预览测试，调试效果请以真机为准。
