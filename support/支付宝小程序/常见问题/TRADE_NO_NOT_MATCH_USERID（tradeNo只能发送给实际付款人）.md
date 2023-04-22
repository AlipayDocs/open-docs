## 错误码
TRADE_NO_NOT_MATCH_USERID（tradeNo只能发送给实际付款人）。 

## 问题描述
小程序调用 alipay.open.app.mini.templatemessage.send（小程序发送模板消息）报错 "code":"40004","msg":"Business Failed","subCode":"TRADE_NO_NOT_MATCH_USERID","subMsg":"tradeNo只能发送给实际付款人"。 

## 涉及接口
[alipay.open.app.mini.templatemessage.send](https://opendocs.alipay.com/mini/02cth2)（小程序发送模板消息）

## 问题原因

- form_id 入参的 tradeNo 支付宝交易号与 to_user_id 入参不是来自同一个用户。
- form_id 入参的 tradeNo 支付宝交易号没有真正支付，没有产生已付款记录。 

## 解决方案

- 检查 form_id 入参是否有误，少写、多写、有多余符号等。
- 检查接口中传入的消息接收方的 to_user_id 与 form_id入参的 tradeNo 是否来自同一个用户。
- form_id 入参的 tradeNo 支付宝交易号必须是已经支付成功的支付宝交易号，tradeNo 支付宝交易号可使用 [小程序支付](https://opendocs.alipay.com/mini/repo-01evwl)产品获取。

 
