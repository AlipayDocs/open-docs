## 错误码
USER_TEMPLATE_LACK_KEYWORD（缺少关键词）。 

## 问题描述
小程序调用 alipay.open.app.mini.templatemessage.send（小程序发送模板消息）报错 "code":"40004","msg":"Business Failed","subCode":"USER_TEMPLATE_LACK_KEYWORD","subMsg":"缺少关键词"。 

## 涉及接口
[alipay.open.app.mini.templatemessage.send](https://opendocs.alipay.com/mini/02cth2)（小程序发送模板消息）

## 问题原因
调用接口发送 data 中的关键词入参个数与开放平台模板库申请的模板关键词个数不一致。 

## 解决方案
申请的模板关键词必须和上送的关键词匹配，例如在申请模板中选择了 5 个关键词，则 data 数据域必须有 keyword1~keyword5 的对象和 value。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/8295e0de-8b2a-4a40-bf5a-fedf5488bac0.png#align=left&display=inline&height=848&margin=%5Bobject%20Object%5D&originHeight=848&originWidth=1500&status=done&style=none&width=1500)<br /> <br /> 
