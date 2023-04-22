## 错误码
VERSION_EXCEEDED_LENGTH

## 错误描述
第三方应用在构建商家小程序时报 VERSION_EXCEEDED_LENGTH（版本号单个数字最大为 2147483647）。

## 涉及接口
[alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）

## 报错原因
alipay.open.mini.version.upload 中传入的 app_version 数字过大导致报错。

## 解决方案
alipay.open.mini.version.upload 中传入的 app_version 不能大于 2147483647。
