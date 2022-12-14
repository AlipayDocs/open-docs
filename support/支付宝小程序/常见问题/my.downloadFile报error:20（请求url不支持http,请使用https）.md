## 错误码
20

## 报错描述
my.downloadFile 下载文件资源到本地时或进行 my.request 网络请求报 error:20，errorMessage:"请求url不支持http,请使用https 。

## 涉及接口

- [my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r)
- [my.request](https://opendocs.alipay.com/mini/api/owycmh)

## 报错原因
URL 参数请求连接使用的是 HTTP 导致。

## 解决方案

- URL 参数请求连接更换成 HTTPS。<br />**注意：**小程序必须使用 HTTPS/WSS 发起网络请求。请求时系统会对服务器域名使用的 HTTPS 证书进行校验，如果校验失败，则请求不能成功发起。由于系统限制，不同平台对于证书要求的严格程度不同。为了保证小程序的兼容性，建议开发者按照最高标准进行证书配置，并使用相关工具检查现有证书是否符合要求。
- 小程序只支持 HTTPS 域名配置。 相比于 HTTP，HTTPS 可以提供更加优质保密的信息，保证了用户数据的安全性，此外 HTTPS 同时也一定程度上保护了服务端，使用恶意攻击和伪装数据的成本大幅提高。因此小程序强制使用 HTTPS，还在使用 HTTP 协议的开发者需要尽快对服务器进行升级，推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)。
