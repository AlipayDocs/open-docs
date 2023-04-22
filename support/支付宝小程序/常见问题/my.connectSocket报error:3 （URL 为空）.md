## 错误码
3

## 报错描述
my.connectSocket 创建一个 [WebSocket](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket) 的连接报错 error:3,errorMessage:URL 为空。

## 涉及接口
[my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3)

## 报错原因
URL 参数入参服务器地址为空所导致。

## 解决方案
确认URL 入参服务器地址是否正常入参填写，URL 必须以 ws 或者 wss 开头。<br />**注意：**部分新发布的小程序只支持 wss 协议。
