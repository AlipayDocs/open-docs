## 错误码
10

## 报错描述
my.sendSocketMessage 通过 WebSocket 连接发送数据消息时报错 error: 10,errorMessage: 没有建连成功之前无法发送消息。

## 涉及接口

- [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3)
- [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1)

## 报错原因
WebSocket 连接与服务器还未建立连接或连接断开，导致 my.sendSocketMessage 发送数据消息报错 error:10（没有建连成功之前无法发送消息）。

## 解决方案
请正常连接服务器后再 my.sendSocketMessage 发送数据消息，可通过 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 监听来判断是否正确与服务器建立连接。<br />**注意：**通过 WebSocket 连接发送数据，需要先使用 [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) 发起建连，并在 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 回调之后再 [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1) 发送数据。
