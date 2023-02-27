# 错误码
VERSION_DESC_IS_BLANK（小程序版本描述为空）。 

# 问题描述
代商家调用 alipay.open.mini.version.audit.apply（小程序提交审核）提交小程序审核时报错 "subCode":"VERSION_DESC_IS_BLANK","subMsg":"小程序版本描述为空"。 

# 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）

# 解决方案
请输入小程序版本描述，检查 version_desc 参数是否入参，小程序版本描述为必填参数，内容在 30-500 个字符之间。<br /> <br /> 
