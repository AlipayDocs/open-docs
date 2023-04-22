
## 问题分析
- 接口设置 SSL 证书设置不正确或者已过期。
- 如果是服务端为 PHP 语言，接口响应内容是否携带 bom 头。
- 请求状态码为 304。 

## 解决方法
保证 SSL 证书链完整并且证书不过期，推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)。

- 去除 bom 头。
- Android 不支持 304 状态，必须是 200 状态。
