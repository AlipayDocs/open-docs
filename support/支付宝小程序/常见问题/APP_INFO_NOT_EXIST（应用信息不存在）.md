# 错误码
APP_INFO_NOT_EXIST（应用信息不存在）。 

# 错误描述
接口报 APP_INFO_NOT_EXIST（应用信息不存在）。 

# 涉及接口

- [alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）
- alipay.commerce.educate.scene.config.create（一脸通行服务配置申请）
- [alipay.open.mini.experience.create](https://opendocs.alipay.com/mini/03l9bw)（小程序生成体验版）
- [alipay.open.mini.version.offline](https://opendocs.alipay.com/mini/03l8c0)（小程序下架）
- [alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）
- [alipay.open.agent.create](https://opendocs.alipay.com/isv/04eh3h)（开启代商户签约、创建应用事务）
- [alipay.open.mini.version.rollback](https://opendocs.alipay.com/mini/03l21q)（小程序回滚）
- alipay.open.mini.widget.goods.upload（小部件商品上传）
- [alipay.open.mini.version.online](https://opendocs.alipay.com/mini/03l21p)（小程序上架）
- [alipay.open.mini.baseinfo.query](https://opendocs.alipay.com/mini/03l21r)（查询小程序基础信息）
- [alipay.open.app.api.field.apply](https://opendocs.alipay.com/isv/04elk6)（申请获取接口用户敏感信息字段）
- [alipay.open.mini.version.audited.cancel](https://opendocs.alipay.com/mini/03l9bs)（小程序退回开发）
- alipay.open.mini.widget.goods.modify（小部件商品修改）
- [alipay.open.mini.version.audit.cancel](https://opendocs.alipay.com/mini/03l9br)（小程序撤销审核）
- alipay.open.mini.widget.data.sync（小程序橱窗数据同步）

# 报错原因

- alipay.open.mini.version.upload 传入的 app_auth_token 错误。
- template_id 参数的入参值有误。

# 解决方案

- alipay.open.mini.version.upload 检查传入的 app_auth_token 是否正确，授权状态是否生效。
- template_id 参数的入参值需要入参对应小程序模板的 APPID，检查是否正确（不要填写第三方应用和商家小程序应用的 APPID）。
