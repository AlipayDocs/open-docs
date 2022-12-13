## 错误码
2 

## 报错描述
HTTP 请求，my.request 网络请求报 error: 2（参数错误）。 

## 涉及接口
[my.request](https://opendocs.alipay.com/mini/api/owycmh) 

## 报错原因
my.request 网络请求，请求链接拼接过长，入参 data 格式有误导致。 

## 解决方案

- 可能是链接过长导致，建议参数放在 data 中处理。
- 建议检查请求时传递的数据是否正常、格式是否正确，可以在请求前打印入参数据日志。

 <br /> 
