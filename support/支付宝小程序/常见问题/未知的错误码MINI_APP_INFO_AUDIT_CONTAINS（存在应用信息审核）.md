## 错误码
未知的错误码 MINI_APP_INFO_AUDIT_CONTAINS（存在应用信息审核）。

## 问题描述
代商家调用 alipay.open.mini.version.audit.apply(小程序提交审核)提交小程序审核时报错 "sub_code":"unknown-sub-code","sub_msg":"未知的错误码MINI_APP_INFO_AUDIT_CONTAINS"。

## 问题原因
在调用提交小程序审核接口前，修改过应用信息，并处于审核中状态导致。

## 涉及接口

- [alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）
- [alipay.open.mini.baseinfo.modify](https://opendocs.alipay.com/mini/03l8c5) (小程序修改基础信息)

## 解决方案

- 耐心等待应用信息审核结束，再调用提交小程序审核接口。
- 信息审核相关疑问咨询可到 [商家服务中心](https://b.alipay.com/index2.htm) 在线咨询或拨打商家客服电话咨询：4007585858，服务时间：8:00-24:00。
