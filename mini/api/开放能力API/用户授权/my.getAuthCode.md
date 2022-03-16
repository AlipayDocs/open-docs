
# 简介
**my.getAuthCode** 是调用接口获取授权码（authCode）的 API。通过授权码可进而换取支付宝用户登录态信息、给用户发会员卡等，从而方便地获取支付宝用户身份标识，快速建立小程序内的用户体系。

登录流程时序等更多介绍信息请参见 [用户授权](https://opendocs.alipay.com/mini/introduce/authcode)。

相关问题请参见 [用户授权 FAQ](https://opendocs.alipay.com/mini/api/bpubha) 。

## 使用限制

- 请勿在小程序的可重复触发的生命周期（例如 onShow）中调用 my.getAuthCode，授权弹窗的消失会触发小程序的 onShow 事件，若接入方未对是否已展现过授权做标识与逻辑判断，将引起重复触发授权。
- 为了创造更良好的支付宝小程序用户体验，在小程序的首屏引导用户授权是不被允许的。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。
- 小程序 **不支持** 使用拼接授权链接进行授权，建议使用 my.getAuthCode 实现用户授权、用户登录等。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/1cdfd0855a5b2beb9466386548165516.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-get-auth-code?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .js 示例代码
```javascript
// .js
// 示例一
my.getAuthCode({
  scopes: 'auth_user',
  success: (res) => {
    my.alert({
      content: res.authCode,
    });
  },
});
// 示例二
my.getAuthCode({
  scopes: ['auth_user'],
  success: (res) => {
    my.alert({
      content: res.authCode,
    });
  },
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| scopes | String/Array | 否 | 授权类型，默认 auth_base。支持 auth_base（静默授权）/ auth_user（主动授权）/ auth_zhima （获取用户芝麻信息）。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### scopes 说明
一个 scope 表示开发者需要请求用户授权的权限范围，一个 scope 包含至少一个 OpenAPI 接口或者 JSAPI 接口。

scopes 可传单个 scope 名称（如 "auth_base"），也可传多个 scope 数据（如 ["auth_user", "auth_zhima"]）。

| **scopes** | **描述** | **包含的服务端 API 接口** |
| --- | --- | --- |
| auth_base | 静默授权，不会发起授权浮窗。在支付宝客户端获取 auth_code，传入服务端调用 [alipay.system.oauth.token](https://opendocs.alipay.com/mini/02qkj4)（换取授权访问令牌接口）获取支付宝会员标识（user_id）。 | 无 |
| auth_user | 主动授权，需要用户手动点击同意，用户同意后，用于 **网站支付宝登录** 和 **获取用户信息**（现已升级为 [获取会员基础信息](https://opendocs.alipay.com/mini/introduce/twn8vq)，且新功能包不再使用 alipay.user.info.share 接口）功能。 | [alipay.user.info.share](https://opendocs.alipay.com/open/02dvf6) |


### success 回调函数
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| authCode | String | 授权码。 |
| authErrorScopes | Key-Value | 失败的授权类型，key 是授权失败的 scope，value 是对应的错误码。 |
| authSuccessScopes | Array | 成功的授权 scope |


## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 4 | 无权限调（N22104）。 | <br />1. 确认小程序应用是否授权给了三方应用，三方应用是否添加了 **JSAPI 基础包** 功能包，可尝试添加 **JSAPI 基础包** 功能包后，重新授权、重新推送预览调试或者直接解除三方应用授权，重新推送预览调试。<br />**说明：** 小程序应用授权给三方应用后，小程序在真机上的运行使用的是三方应用的功能包，不再是使用小程序自身的功能包。<br /> 2. 若是小程序应用 **JSAPI 基础包** 功能包没有或者不全，建议删除小程序应用，重新创建一个新的小程序应用来调试。|
| 10 | Empty Data | <br /><ul><li>为了创造更良好的支付宝小程序用户体验，在小程序的首屏引导用户授权是不被允许的。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。</li><li>检查 scopes 入参是否正确（参数错误会先弹出“服务正忙，请稍后再试”）。</li><li>建议在需要获取用户信息前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。</li><li>在 fail 做引导处理，重新调用 my.getAuthCode 授权。</li></ul> |
| 11 | 用户取消授权 | <br /><ul><li>为了创造更良好的支付宝小程序用户体验，在小程序的首屏引导用户授权是不被允许的。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。</li><li>建议在需要获取用户信息前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。</li><li>在 fail 做引导处理，重新调用 my.getAuthCode 授权。</li></ul> |

