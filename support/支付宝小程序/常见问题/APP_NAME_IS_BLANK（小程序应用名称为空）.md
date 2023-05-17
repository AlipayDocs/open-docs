## 错误码
APP_NAME_IS_BLANK（小程序应用名称为空）。

## 错误描述
alipay.open.mini.version.audit.apply(小程序提交审核) 报 APP_NAME_IS_BLANK（小程序应用名称为空）。

## 涉及接口

[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）

## 解决方案
当前小程序没有设置小程序名称或者当前小程序名称已释放，提交审核时需要传入 app_name 参数。
