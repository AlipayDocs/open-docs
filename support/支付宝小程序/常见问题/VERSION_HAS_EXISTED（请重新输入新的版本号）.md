## 错误码
VERSION_HAS_EXISTED

## 错误描述
第三方应用在构建商家小程序时报 VERSION_HAS_EXISTED（请重新输入新的版本号）。

## 涉及接口
[alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）

## 报错原因
alipay.open.mini.version.upload 中参数 app_version 设置不符合入参要求导致。

## 解决方案
在 alipay.open.mini.version.upload 中修改 app_version 参数，app_version 要大于之前的版本。
