## 错误码
USER_KEYWORD_LENGTH_ERROR（关键词超长）。 

## 问题描述
小程序调用 alipay.open.app.mini.templatemessage.send（小程序发送模板消息）发送模板消息报错 "code":"40004","msg":"Business Failed","subCode":"USER_KEYWORD_LENGTH_ERROR","subMsg":"关键词超长"。 

## 涉及接口
[alipay.open.app.mini.templatemessage.send](https://opendocs.alipay.com/mini/02cth2)（小程序发送模板消息）

## 解决方案
调用接口上送 data 入参中的每个关键词的 value 值长度不得大于 50 个字符，请修改 keyword.value 的入参。
