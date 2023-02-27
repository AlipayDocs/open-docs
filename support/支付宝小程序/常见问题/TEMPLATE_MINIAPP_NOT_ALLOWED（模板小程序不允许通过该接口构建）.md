## 错误码
TEMPLATE_MINIAPP_NOT_ALLOWED（模板小程序不允许通过该接口构建）

## 错误描述
第三方应用在构建商家小程序时报 TEMPLATE_MINIAPP_NOT_ALLOWED（模板小程序不允许通过该接口构建）。

## 涉及接口
[alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）

## 报错原因
alipay.open.mini.version.upload 传入的 app_auth_token 为小程序模板授权 token。

## 解决方案
alipay.open.mini.version.upload 的 app_auth_token 需要传入商家小程序的授权 token。小程序模板并不能通过构建接口来构建小程序模板版本。
