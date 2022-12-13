## 错误码
5

## 报错描述
my.connectSocket 创建一个 [WebSocket](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket) 的连接时报错 error:5,errorMessage:URL 地址不是ws或者wss.。 

## 涉及接口
[my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) 

## 报错原因
URL 参数入参服务器地址不是 ws 或者 wss 协议导致。 

## 解决方案
确认 URL 入参服务器地址协议是否正确，URL 必须以 ws 或者 wss 开头。<br />**注意：**部分新发布的小程序只支持 wss 协议。 <br /> 
