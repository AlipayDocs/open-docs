## 错误码
SERVICE_TEL_AND_MAIL_BOTH_BLANK（小程序客服电话和邮箱同时为空）。 

## 错误描述
alipay.open.mini.version.audit.apply（小程序提交审核接口）报 SERVICE_TEL_AND_MAIL_BOTH_BLANK（小程序客服电话和邮箱同时为空）。 

## 涉及接口

- [alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）
- [alipay.open.mini.baseinfo.modify](https://opendocs.alipay.com/mini/03l8c5) (小程序修改基础信息)

## 解决方案
小程序客服邮箱 service_email 和小程序客服电话 service_phone 至少传入一个。<br /> <br /> 
