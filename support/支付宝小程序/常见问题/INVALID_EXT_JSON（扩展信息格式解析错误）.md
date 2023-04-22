## 错误码
INVALID_EXT_JSON（扩展信息格式解析错误）。

## 错误描述
第三方应用在构建商家小程序时报 INVALID_EXT_JSON（扩展信息格式解析错误）。

## 涉及接口
[alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）

## 报错原因
alipay.open.mini.version.upload 中传入的 ext 扩展信息参数不是标准的 JSON 字符串。

## 解决方案
修改 alipay.open.mini.version.upload 中传入的 ext 为标准的 JSON 字符串。
