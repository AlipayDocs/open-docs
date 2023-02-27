## 错误码
MINI_APP_MEMO_SENSITIVE（小程序备注存在敏感词）

## 错误描述
alipay.open.mini.version.audit.apply(小程序提交审核) 报 MINI_APP_MEMO_SENSITIVE（小程序备注存在敏感词）。

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）

## 解决方案
传入的 memo 存在敏感词，需去除敏感词后重新提交审核，可参考 [小程序审核规范](https://opendocs.alipay.com/b/03ajj7)。
