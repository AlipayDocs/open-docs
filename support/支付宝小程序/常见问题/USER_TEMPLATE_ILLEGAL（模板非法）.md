## 错误码
USER_TEMPLATE_ILLEGAL（模板非法）。 

## 问题描述
小程序调用 alipay.open.app.mini.templatemessage.send（小程序发送模板消息）发送模板消息报错 "code":"40004","msg":"Business Failed","subCode":"FORM_ID_NOT_MATCH_APPID","subMsg":"formId和appId不匹配"。 

## 涉及接口
[alipay.open.app.mini.templatemessage.send](https://opendocs.alipay.com/mini/02cth2)（小程序发送模板消息）

## 解决方案

- 确认 templateId 是否和申请的模板 Id 匹配；同时需要确认该模板是否已经被删除。
- 检查后台配置的模板是表单类型还是交易类型，交易类型模板 form_id 请传当前小程序应用的支付订单 tradeNo 交易号，表单类型模板 form_id 请传递当前小程序应用前端 form 表单组件返回的 formId（**IDE开发工具上产生的formId不生效，请使用真机上产生的formId**）。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/1144d57d-258c-4d43-a969-422c8178ea3e.png#align=left&display=inline&height=309&margin=%5Bobject%20Object%5D&originHeight=309&originWidth=746&status=done&style=none&width=746)
