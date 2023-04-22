## 错误码
TEMPLATE_ID_IS_BLANK

## 错误描述
三方应用在构建商家小程序时报 TEMPLATE_ID_IS_BLANK（模板id为空）。

## 涉及接口
alipay.open.mini.version.upload（小程序基于模板上传版本）。<br />alipay.open.mini.template.usage.query （查询使用模板的小程序列表）<br />alipay.open.mini.version.upload（小程序基于模板上传版本）

## 报错原因
alipay.open.mini.version.upload 没有传 template_id参数。

## 解决方案
alipay.open.mini.version.upload 中传入有效的 template_id参数。
