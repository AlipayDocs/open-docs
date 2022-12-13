## 错误码
10

## 报错描述
my.getAuthCode 用户授权获取用户信息 fail 返回 error：10，errorMessage："Empty Data"。 

## 涉及接口
[my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize)

## 报错原因

- my.getAuthCode 唤起用户信息授权弹窗时，用户没有点击“拒绝”或“同意”关闭弹窗或点击退回键。
- scopes 入参有误。
- 没有进行授权，切换小程序到后台后从其它入口再次进入小程序。 

## 解决方案

- 为了创造更良好的支付宝小程序用户体验，在小程序的首屏引导用户授权是不被允许的。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。
- 检查 scopes 入参是否正确，详情请查看 [入参参数列表](https://opendocs.alipay.com/mini/api/openapi-authorize#%E5%85%A5%E5%8F%82)（参数错误会先弹出“**服务正忙，请稍后再试**”）。
- 建议在需要获取用户信息前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。在 fail 做引导处理，重新调用 my.getAuthCode 授权。

 
