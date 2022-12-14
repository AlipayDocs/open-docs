## 错误码
11

## 报错描述
my.rsa 非对称加密数据时 fail 返回 error：11，errorMessage："Encrypt key error"。

## 涉及接口
[my.rsa](https://opendocs.alipay.com/mini/api/data-safe)

## 报错原因
入参字段 key 不完整、缺失、错误导致。

## 解决方案

1. 确保 key 正确，可以使用工具验证 RSA 密钥是否匹配完整，下载 [开放平台密钥工具](https://opendocs.alipay.com/common/02kipk)。<br />
2. 使用下载的密钥工具重新生成一对完整的密钥。
