## 错误码
10

## 报错描述
my.rsa 非对称加密数据时 fail 返回：<br />error：10，errorMessage："h5RSA param action must be encrypt/decrypt"<br />error：10，errorMessage："h5RSA params (text and key) must not be empty"<br />

## 涉及接口
[my.rsa](https://opendocs.alipay.com/mini/api/data-safe)

## 报错原因
入参缺少必要参数 action、text、key 导致。

## 解决方案

- 检查 action、text、key 必填参数是否都有入参。
- action 参数入参必须是 encrypt（加密）或 decrypt（解密）。
- key 参数入参可以使用工具生成 RSA 密钥并获取 key，下载 [开放平台密钥工具](https://opendocs.alipay.com/common/02kipk)。详情接入可参考[小程序RSA非对称加密/解密](https://opendocs.alipay.com/support/01rb0d)。
