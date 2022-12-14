## 错误描述
接口报错 APPLICATION_TYPE_NOT_MINIAPP（该应用不是小程序类型）。

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
- [alipay.open.app.members.delete](https://opendocs.alipay.com/mini/03l3ex)（应用删除成员）
- [alipay.open.mini.safedomain.create](https://opendocs.alipay.com/mini/03l9by)（小程序添加域白名单）
- [alipay.open.mini.baseinfo.modify](https://opendocs.alipay.com/mini/03l8c5)（小程序修改基础信息）
- [alipay.open.mini.baseinfo.query](https://opendocs.alipay.com/mini/03l21r)（查询小程序基础信息）
- [alipay.open.mini.version.list.query](https://opendocs.alipay.com/mini/03l9bv)（小程序版本列表查询）
- alipay.open.mini.privacy.audit.create（小程序创建隐私协议）
- [alipay.open.app.members.create](https://opendocs.alipay.com/mini/03l21t)（应用添加成员）
- [alipay.open.app.members.query](https://opendocs.alipay.com/mini/03l3ew)（应用查询成员列表）
- [alipay.open.mini.safedomain.delet](https://opendocs.alipay.com/mini/03l3f0)（小程序删除域白名单）

## 报错原因
APPID 对应的应用不是小程序应用。

## 解决方案
确保创建的应用是小程序应用，且入参的 APPID，是小程序应用的 APPID。
