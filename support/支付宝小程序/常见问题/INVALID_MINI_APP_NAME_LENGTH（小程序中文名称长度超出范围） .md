## 错误码
INVALID_MINI_APP_NAME_LENGTH（小程序中文名称长度超出范围）。 

## 错误描述
alipay.open.mini.version.audit.apply(小程序提交审核) 报 INVALID_MINI_APP_NAME_LENGTH（小程序中文名称长度超出范围）。 

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）<br />alipay.open.mini.isv.create（isv服务商代商户创建小程序）<br />alipay.open.mini.baseinfo.modify（小程序修改基础信息）<br />alipay.open.agent.mini.create（代商家创建小程序应用）

## 解决方案
app_name 过长导致，将 app_name 限制在 3-20 个字符之内即可。<br /> 
