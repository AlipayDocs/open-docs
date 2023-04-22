## 错误码
MINI_APP_PACKAGE_INFO_NOT_EXIST（小程序版本包信息不存在）

## 问题原因
调用提交审核、设置生成体验版、上架、灰度等接口时，所传入的参数 app_version 小程序版本号有误，导致获取不到对应版本的包信息。

## 涉及接口

- [alipay.open.mini.version.online](https://opendocs.alipay.com/mini/03l21p)（小程序上架）
- [alipay.open.mini.experience.cancel](https://opendocs.alipay.com/mini/03l8c4)（小程序取消体验版）
- [alipay.open.mini.version.rollback](https://opendocs.alipay.com/mini/03l21q)（小程序回滚）
- [alipay.open.mini.experience.create](https://opendocs.alipay.com/mini/03l9bw)（小程序生成体验版）
- [alipay.open.mini.version.audited.cancel](https://opendocs.alipay.com/mini/03l9bs)（小程序退回开发）
- [alipay.open.mini.version.offline](https://opendocs.alipay.com/mini/03l8c0)（小程序下架）
- [alipay.open.mini.version.gray.cancel](https://opendocs.alipay.com/mini/03l9bt)（小程序结束灰度）
- [alipay.open.mini.version.gray.online](https://opendocs.alipay.com/mini/03l3ev)（小程序灰度上架）
- [alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）
- [alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）
- [alipay.open.mini.experience.query](https://opendocs.alipay.com/mini/03l8c3)（小程序体验版状态查询接口）
- [alipay.open.mini.version.audit.cancel](https://opendocs.alipay.com/mini/03l9br)（小程序撤销审核）

## 解决方案

- 请确认是否已经删除或者不存在该版本，调用 [alipay.open.mini.version.detail.query](https://opendocs.alipay.com/mini/03l9bu)（小程序版本详情查询）查询该版本信息是否存在以及 status 小程序版本状态是否正常符合调用接口要求。
- 如果调用 [alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）后直接调用了提交审核或生成体验版本接口，请调用 [alipay.open.mini.version.build.query](https://opendocs.alipay.com/mini/03l3es)（小程序查询版本构建状态）确认版本构建成功后再做后续操作。**<br />注意：**
   - 2019年以前创建的小程序，并且之前上传过版本或上架过（走的openhome创建，并且曾经从IDE上传过版本，都不会走升级的配置化构建模式），在三方代构建小程序版本时还是走实例化构建模式。<br />
   - 不论是实例化构建模式还是升级后配置化构建模式，都应在调用构建版本的接口后 [查询构建状态](https://opendocs.alipay.com/isv/03kqzl#%E6%9F%A5%E8%AF%A2%E5%95%86%E5%AE%B6%E5%B0%8F%E7%A8%8B%E5%BA%8F%E6%9E%84%E5%BB%BA%E7%8A%B6%E6%80%81)，查询到构建成功再进行后续操作。
