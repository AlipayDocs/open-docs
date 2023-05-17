## 错误码
MINI_APP_SLOGAN_SENSITIVE（小程序应用简介存在敏感词）

## 错误描述
alipay.open.mini.version.audit.apply（小程序提交审核）报 MINI_APP_SLOGAN_SENSITIVE（小程序应用简介存在敏感词）。

## 涉及接口

- [alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）
- [alipay.open.mini.baseinfo.modify](https://opendocs.alipay.com/mini/03l8c5)（小程序修改基础信息）

## 解决方案
传入的 app_slogan 存在敏感词，需去除敏感词后重新提交审核，可参考 [小程序简介审核规范](https://opendocs.alipay.com/b/03ajj7#2.%20%E5%9F%BA%E7%A1%80%E4%BF%A1%E6%81%AF%E8%A7%84%E8%8C%83)。
