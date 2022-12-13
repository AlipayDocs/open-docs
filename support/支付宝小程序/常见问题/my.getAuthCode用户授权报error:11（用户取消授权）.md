## 错误码
11

## 报错描述
my.getAuthCode 用户授权获取用户信息 fail 返回 error：11，errorMessage："用户取消授权"。 

## 涉及接口
[my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize)

## 报错原因
my.getAuthCode 唤起用户信息授权弹窗时，用户点击 **拒绝** 按钮拒绝授权用户信息给小程序。 

## 解决方案

- 为了创造更良好的支付宝小程序用户体验，在小程序的首屏引导用户授权是不被允许的。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。
- 建议在需要获取用户信息前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。
- 在 fail 做引导处理，重新调用 my.getAuthCode 授权。
