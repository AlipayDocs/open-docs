# 错误码
CODE_TEMPLATE_DELETED

## 错误描述
三方应用在构建商家小程序时报 CODE_TEMPLATE_DELETED（指定的代码模板已经删除）。

## 涉及接口
[alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）

## 报错原因
alipay.open.mini.version.upload 传入的 template_id 已经删除。

## 解决方案
alipay.open.mini.version.upload 需要传入审核通过状态的 template_id。
