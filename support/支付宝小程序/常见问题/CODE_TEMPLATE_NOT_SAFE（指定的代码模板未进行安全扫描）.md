## 错误码
CODE_TEMPLATE_NOT_SAFE

## 错误描述
三方应用在构建商家小程序时报 CODE_TEMPLATE_NOT_SAFE（指定的代码模板未进行安全扫描）。

## 涉及接口
[alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）

## 报错原因
alipay.open.mini.version.upload 传入的 template_id 未通过安全扫描。

## 解决方案
等待传入的模板安全扫描后再调用 alipay.open.mini.version.upload。
