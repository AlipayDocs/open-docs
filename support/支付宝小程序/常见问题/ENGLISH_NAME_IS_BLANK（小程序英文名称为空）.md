## 错误码
ENGLISH_NAME_IS_BLANK（小程序英文名称为空）。 

## 错误描述
alipay.open.mini.version.audit.apply（小程序提交审核接口）报 ENGLISH_NAME_IS_BLANK（小程序英文名称为空）。 

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）<br />alipay.open.agent.mini.create （代商家创建小程序应用）

## 解决方案
app_english_name 为可选参数，不传该参数时默认使用当前小程序英文名称，但如果当前小程序没有设置英文名称则会出现此报错，此时提交审核时需要传入 app_english_name 参数。<br /> <br /> 
