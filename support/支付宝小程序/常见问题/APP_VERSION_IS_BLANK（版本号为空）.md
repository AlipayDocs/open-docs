## 错误码
APP_VERSION_IS_BLANK

## 错误描述
三方应用在构建商家小程序时报 APP_VERSION_IS_BLANK（版本号为空）。

## 涉及接口

- [alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）
- [alipay.open.mini.version.detail.query](https://opendocs.alipay.com/mini/03l9bu)（小程序版本详情查询）
- [alipay.open.mini.version.audited.cancel](https://opendocs.alipay.com/mini/03l9bs)（小程序退回开发）
- [alipay.open.mini.version.gray.online](https://opendocs.alipay.com/mini/03l3ev)（小程序灰度上架）
- [alipay.open.mini.version.gray.cancel](https://opendocs.alipay.com/mini/03l9bt)（小程序结束灰度）
- [alipay.open.mini.version.online](https://opendocs.alipay.com/mini/03l21p)（小程序上架）
- [alipay.open.mini.version.offline](https://opendocs.alipay.com/mini/03l8c0)（小程序下架）
- [alipay.open.mini.version.rollback](https://opendocs.alipay.com/mini/03l21q)（小程序回滚）
- [alipay.open.mini.version.delete](https://opendocs.alipay.com/mini/03l8c2)（小程序删除版本）
- [alipay.open.mini.experience.cancel](https://opendocs.alipay.com/mini/03l8c4)（小程序取消体验版）
- [alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）
- [alipay.open.mini.version.audit.cancel](https://opendocs.alipay.com/mini/03l9br)（小程序撤销审核）
- [alipay.open.mini.experience.query](https://opendocs.alipay.com/mini/03l8c3)（小程序体验版状态查询）
- [alipay.open.mini.version.build.query](https://opendocs.alipay.com/mini/03l3es)（小程序查询版本构建状态）
- [alipay.open.mini.experience.create](https://opendocs.alipay.com/mini/03l9bw)（小程序生成体验版）

## 报错原因
没有传 app_version 参数或参数值为空、不正确。

## 解决方案

- 检查接口入参，传入有效的 app_version 参数。
- 确认需要操作/查询的版本是否已经构建成功，建议调用 [alipay.open.mini.version.build.query](https://opendocs.alipay.com/mini/03l3es)（小程序查询版本构建状态）确认版本的构建状态。

**注意：**调用 alipay.open.mini.version.upload（小程序基于模板上传版本）构建版本后，建议确认版本构建状态后再做下一步操作。
