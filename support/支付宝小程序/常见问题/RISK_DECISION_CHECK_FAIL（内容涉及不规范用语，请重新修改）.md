## 问题描述
调用报：RISK_DECISION_CHECK_FAIL（内容涉及不规范用语，请重新修改）。

## 问题原因
这种情况一般是因为名称、描述、简介等应用信息存在敏感词被风控拦截导致。

## 涉及接口
alipay.open.mini.version.audit.apply（小程序提交审核）<br />alipay.open.mini.baseinfo.modify（小程序修改基础信息）<br />alipay.open.agent.mini.create（代商家创建小程序应用）

## 解决方案
名称、描述、简介等应用信息存在敏感词被风控拦截，建议开发者修改信息，确保名称等文字不存在风险词汇，详情请查看 [运营规范](https://opendocs.alipay.com/b/03al2i)。
