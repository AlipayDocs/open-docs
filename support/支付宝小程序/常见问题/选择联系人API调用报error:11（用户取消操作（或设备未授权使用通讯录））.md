# 错误码
11 

## 报错描述
选择联系人API调用报 error:11，errorMessage："用户取消操作（或设备未授权使用通讯录）"。 

## 涉及接口

- [my.chooseAlipayContact](https://opendocs.alipay.com/mini/api/ui-contact)
- [my.choosePhoneContact](https://opendocs.alipay.com/mini/api/blghgl)

## 报错原因
唤起通讯录选择联系人时，用户没有选择联系人就左上角返回或返回键返回小程序，用户取消操作。 

## 解决方案
为了创造更良好的支付宝小程序用户体验，建议在选择联系人前增加引导提示，提升用户体验。<br />在 fail 做引导处理，重新调用联系人 API 选择通讯录中的联系人。<br /> 
