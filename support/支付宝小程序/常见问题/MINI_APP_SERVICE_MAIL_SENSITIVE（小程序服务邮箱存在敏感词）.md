## 错误码
MINI_APP_SERVICE_MAIL_SENSITIVE（小程序服务邮箱存在敏感词）

## 错误描述
alipay.open.mini.version.audit.apply(小程序提交审核) 报 MINI_APP_SERVICE_MAIL_SENSITIVE（小程序服务邮箱存在敏感词）。

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）<br />alipay.open.agent.mini.create （代商家创建小程序应用）

## 解决方案
传入的服务邮箱 service_email 存在敏感词，需更换邮箱后重新提交审核，可参考 [小程序运营规范](https://opendocs.alipay.com/b/03ajj7)。
