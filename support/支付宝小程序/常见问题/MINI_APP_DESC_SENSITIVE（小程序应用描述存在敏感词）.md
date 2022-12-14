## 错误码
MINI_APP_DESC_SENSITIVE（小程序应用描述存在敏感词）

## 错误描述
接口报 MINI_APP_DESC_SENSITIVE（小程序应用描述存在敏感词）。

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）<br />[alipay.open.mini.baseinfo.modify](https://opendocs.alipay.com/mini/03l8c5)（小程序修改基础信息）

## 解决方案
传入的 app_desc 存在敏感词，需去除敏感词后重新提交审核，可参考 [小程序运营规范](https://opendocs.alipay.com/b/03ajj7)。
