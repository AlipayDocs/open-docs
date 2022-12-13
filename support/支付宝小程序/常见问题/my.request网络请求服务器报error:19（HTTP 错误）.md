## 错误码
19

## 报错描述
HTTP 请求，my.request 网络请求服务器报 error: 19（HTTP 错误）。 

## 涉及接口
[my.request](https://opendocs.alipay.com/mini/api/owycmh)

## 报错原因
my.request 网络请求不能正常访问服务器，使用局域网本地请求、证书不正确等导致 HTTP 错误。 

## 解决方案

- 请确认请求 URL 地址在外网是否能正常请求，HTTPS 协议，小程序真机上都是生产环境的正式请求，不能使用局域网本地请求。
- 一般如 HTTP 404、500、504 等异常错误，建议打开 IDE 调试器 > Network 可以查看具体的错误信息，然后根据对应 HTTP 错误码对症处理。
- SSL 证书不正确导致的，建议更换网站 SSL 证书，推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)。

 <br /> 
