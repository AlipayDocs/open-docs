## 报错描述
my.request 请求服务端报错，回调函数 fail 返回： "error":14,"errorMessage": "JSON parse data error"。 

## 问题原因

- my.request 设置了 dataType=json 或者没有设置 dataType 时，服务端返回响应的结果为非 JSON 字符串就会报此错误。
- 接口设置 SSL 证书设置不正确或者已过期。 

## 解决方案

- 修正服务端响应内容为标准 JSON 字符串。<br />**注意：**如果服务端是 PHP 或 .net，可检查响应的内容中是否携带了 bom，一般是相关代码文件或者配置文件携带 bom，可以搜索引擎搜索 **清除utf-8 bom头**，可在在线接口测试工具上查看是否带 bom。
- 若服务端要返回非 JSON 字符串则需要把 my.request 的 dataType 参数设置成 text。
- 保证 SSL 证书链完整并且证书不过期，推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)，可以使用证书工具或者咨询服务器提供商如阿里云进行验证。

 
