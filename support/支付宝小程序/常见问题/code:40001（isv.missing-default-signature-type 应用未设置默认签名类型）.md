## 错误码
40001 

## 错误描述
获取会员手机号/或运动步数，会员授权后my.getPhoneNumber/my.getRunData返回示例如下。
```
{code：40001,msg:"Missing Required Arguments"，subCode:"isv.missing-encrypt-key",subMsg:"缺少加密配置" }
```

## 涉及接口

- [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber)
- [my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v)

## 问题原因

- 小程序未配置接口加签方式（支付宝公钥）、接口内容加密方式（ AES 密钥）、应用网关导致的报错。
- 服务商代商家获取手机号在调用 [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) 接口时没有入参 protocols#isvAppId（即三方应用 appId）。 

## 解决方案

1. 登录 [支付宝开放平台](https://openhome.alipay.com/mini/dev/list) > 进入小程序详情页 > **开发设置** > **开发信息** 中设置 [接口加签方式](https://opendocs.alipay.com/common/02mriz)、[接口内容加密方式](https://opendocs.alipay.com/common/02mse3)、[应用网关](https://opendocs.alipay.com/common/02qibh)。![](https://cdn.nlark.com/yuque/0/2022/png/179989/1659943780477-b8072e1e-07f0-4ed0-a0c9-22aa7cc04148.png?x-oss-process=image%2Fresize%2Cw_1554#align=left&display=inline&height=784&margin=%5Bobject%20Object%5D&originHeight=784&originWidth=1554&status=done&style=none&width=1554)
2. 服务商代商家解密手机号报错应用未设置默认签名类型，是因为小程序端在调用 [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) 接口时没有入参 protocols#isvAppId（即三方应用 appId）。

示例代码：
```html
my.getPhoneNumber({ 
  protocols: { // 小程序模板所属的三方应用appId
        isvAppId: '三方应用appId'
  },  
  success: (res) => { 
  let encryptedData = res.response;
my.request({
    url: '你的服务端地址',
    data: encryptedData,
  });  
},
fail: (res) => {
  console.log('getPhoneNumber_fail');
  console.log(res);  
  },
});
```

3. 检查设置完成后，点击 小程序右上角三个点 > **关于** > 右上角（设置）> **用户信息**，解除授权后重新授权获取。

