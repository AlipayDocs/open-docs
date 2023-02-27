## 错误描述
my.getPhoneNumber 返回字段中只有 reponse 值，没有返回 sign 值。

## 问题原因
小程序的支付宝公钥、AES密钥，应用网关没有设置导致。

## 解决方案

1. 在开放平台控制台 >** **对应小程序详情页 > **开发设置** 中检查接口加签方式、AES密钥、应用网关是否已经设置，若没有设置可查看相关设置文档进行设置。详情请查看 [接口加签方式说明](https://opendocs.alipay.com/common/02mse2)、[接口内容加密方式](https://opendocs.alipay.com/common/02mse3)、[应用网关](https://opendocs.alipay.com/common/02qibh)；<br />
![7B68F537-9A1C-49b2-8254-5E9DE7C2A911.png](https://cdn.nlark.com/yuque/0/2021/png/179989/1624933096591-8e067bf9-6017-4e5b-8f65-7ebbcf5a76a1.png#align=left&display=inline&height=510&margin=%5Bobject%20Object%5D&name=7B68F537-9A1C-49b2-8254-5E9DE7C2A911.png&originHeight=510&originWidth=829&size=15555&status=done&style=none&width=829)<br />
2. 检查设置完成后，点击 小程序右上角三个点 > **关于** > 再右上角（设置）> 用户信息，解除授权后重新授权获取。
