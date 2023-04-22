## 报错描述
小程序二维码接口 [alipay.open.app.qrcode.create](https://opendocs.alipay.com/mini/03l9b8) 请求报错“ISV权限不足”。<br />报错信息如下：
```
{"alipay_open_app_qrcode_create_response":{
"code":"40006",
"msg":"Insufficient Permissions",
"sub_code":"isv.insufficient-isv-permissions",
"sub_msg":"ISV权限不足，建议在开放平台控制台检查对应产品是否已经绑定
},
"sign":"xxxx"}
```

## 问题原因

- 没有绑定产品。
- 调用接口方法错误。
- 传入的 APPID 错误。 

## 解决方案

- 检查小程序应用里是否绑定在小程序权限集中绑定 **小程序码**。
- 检查请求的接口是否是小程序二维码接口 [alipay.open.app.qrcode.create](https://opendocs.alipay.com/mini/03l9b8)。
- 检查服务端接口请求传入的 APPID 是不是小程序应用的 APPID。
