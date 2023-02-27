## 错误码
FORM_ID_NOT_MATCH_APPID（formId和appId不匹配）。

## 问题描述
小程序调用 alipay.open.app.mini.templatemessage.send（小程序发送模板消息接口）发送模板消息报错 "code":"40004","msg":"Business Failed","subCode":"FORM_ID_NOT_MATCH_APPID","subMsg":"formId和appId不匹配"。 

## 涉及接口
[alipay.open.app.mini.templatemessage.send](https://opendocs.alipay.com/mini/02cth2)（小程序发送模板消息） 

## 解决方案
如果是点击表单产生的 formId，则只允许提供当前表单的小程序使用该 formId 发送，如果是 tradeNo，则允许第一次使用这个 tradeNo 的小程序使用，即 **A 小程序前端生成的formId/支付的订单 tradeNo，不能用于 B 小程序后端调用接口发送模板消息**（如果是三方应用代调用接口，请入参 A 小程序的应用授权 app_auth_token）。<br /> <br /> 
