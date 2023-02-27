## 错误码
INVALID_MINI_APP_SERVICE_TEL（小程序客服电话包含非法字符）。 

## 错误描述
alipay.open.mini.version.audit.apply（小程序提交审核接口）报 INVALID_MINI_APP_SERVICE_TEL（小程序客服电话包含非法字符）。 

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）<br />[alipay.open.agent.mini.create ](https://opendocs.alipay.com/isv/04f74l)(代商家创建小程序应用)

## 解决方案
检查下传入的 service_phone（小程序客服电话），只允许包含数字和 -，且控制在 5-30 个字符之内。<br /> 
