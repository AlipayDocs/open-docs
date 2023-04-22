
## 问题描述
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/isv/03kqzm)（小程序提交审核）接口调用报：CAN_NOT_SUBMIT_WITH_AUDIT_GRAY（存在审核中，审核通过，审核拒绝，灰度中版本不能提审）。;

## 问题原因
该小程序已经存在审核中、审核通过、审核驳回、灰度中状态的版本。一个小程序有且最多只有一个审核中、审核通过、审核驳回、灰度中的版本，这种错误一般是因为之前这个小程序已经提交审核，或者审核通过，被驳回或者已经在灰度中了。

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq) (小程序提交审核)

## 解决方案

- 如果已经存在审核中版本，需要等待审核通过、或者审核驳回（可使用 [alipay.open.mini.version.detail.query](https://opendocs.alipay.com/isv/03kqzm)（小程序版本详情查询）查询版本状态）。
- 如果已经审核被驳回，需要调用 [alipay.open.mini.version.audited.cancel](https://opendocs.alipay.com/mini/03l9bs)（小程序退回开发）。
- 如果已经审核通过，需要调用 [alipay.open.mini.version.audited.cancel](https://opendocs.alipay.com/mini/03l9bs)（小程序退回开发），或者调用 [alipay.open.mini.version.online](https://opendocs.alipay.com/mini/03l21p)（小程序上架）。
- 如果已经灰度中，需要调用 [alipay.open.mini.version.online](https://opendocs.alipay.com/mini/03l21p)（小程序上架）。
