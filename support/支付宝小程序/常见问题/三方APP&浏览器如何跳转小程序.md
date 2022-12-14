三方APP应用跳转小程序目前有两种方式可以跳转。

## scheme拼接方式
加上 `https://ds.alipay.com/?scheme=` 前缀，后面拼接 `alipays://platformapi/startapp?appId=xxx&page=x/y/z&query=xx%3dxx`。<br />详情可查看 [scheme链接介绍](https://opendocs.alipay.com/support/01rb18) 。

## 小程序二维码方式

1. 生成 [小程序二维码](https://opendocs.alipay.com/mini/introduce/qrcode)。
2. 获取二维码包含的内容链接（可以通过三方工具扫一扫二维码获取）。
3. 使用该内容链接跳转。如官方小程序示例的二维码链接：`https://qr.alipay.com/s6x09210ka4u33onnn3sud0`。
