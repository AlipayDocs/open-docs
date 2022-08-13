# 简介

**my.getAuthCode** 是获取授权码（authCode）的 API，通过授权码可换取支付宝用户信息、给用户发会员卡，快速建立小程序内的用户体系。

为了创造更良好的支付宝小程序用户体验，不允许在小程序的首屏引导用户授权。需要在用户充分了解小程序的业务内容后再引导用户授权。

授权码换取支付宝用户信息等更多介绍可查看 [用户授权](https://opendocs.alipay.com/mini/introduce/authcode)。

## 使用限制

- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 此 API 支持在小程序插件中使用，授权主体是宿主小程序。
- 此 API 不支持在 web-view 中使用。如果要在 web-view 中获取用户信息，请在小程序上下文中获取后传递到 web-view 中。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/1cdfd0855a5b2beb9466386548165516.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/get-auth-code?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

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

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| scopes | String/Array | 否 | 授权类型，默认 auth_base。支持 auth_base（静默授权）/ auth_user（主动授权）。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### String/Array scopes

一个 scope 表示开发者需要请求用户授权的权限范围，一个 scope 包含至少一个 OpenAPI 接口或者 JSAPI 接口。

| **scopes** | **功能用法** | **包含的服务端 API 接口** |
| --- | --- | --- |
| auth_base | 授权获取用户唯一标识和授权访问令牌。在支付宝客户端获取 auth_code，传入服务端调用 [alipay.system.oauth.token](https://opendocs.alipay.com/apis/api_9/alipay.system.oauth.token)（换取授权访问令牌接口）获取支付宝会员标识（user_id）。此方式不会弹出授权浮窗。 | alipay.system.oauth.token |
| auth_user | 授权获取支付宝会员信息。在支付宝客户端获取 auth_code，传入服务端调用 [alipay.system.oauth.token](https://opendocs.alipay.com/apis/api_9/alipay.system.oauth.token)（换取授权访问令牌接口）换取授权访问令牌，然后调用  [alipay.user.info.share](https://opendocs.alipay.com/apis/api_2/alipay.user.info.share) （支付宝会员授权信息查询接口）获取用户已授权的信息。| alipay.system.oauth.token、alipay.user.info.share |
### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| authCode | String | 授权码。 |
| authErrorScopes | Object | 失败的授权类型，key 是授权失败的 scope，value 是对应的错误码。 |
| authSuccessScopes | Array | 成功的授权 scope。 |

## 错误码

| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 4 | 无权限调（N22104）。 | <br /><ol><li>确认小程序应用是否授权给了三方应用，三方应用是否添加了 <b>JSAPI 基础包</b> 功能包。<br /><b>说明</b>：小程序应用授权给三方应用后，小程序在真机上的运行使用的是三方应用的功能包，不再是使用小程序自身的功能包。</li><li>若是小程序应用 <b>JSAPI 基础包</b> 功能包没有或者不全，建议删除小程序应用，重新创建一个新的小程序应用来调试。</li></ol>|
| 3 | 未找到授权结果 | <ol><li>因为 scopes 入参错误导致数据获取不到（参数错误会先弹出 <b>服务正忙，请稍后再试</b>），检查 scopes 入参是否正确。</li><li>用户关闭弹窗导致数据获取不到，可在 fail 回调中做引导授权，重新调用 my.getAuthCode 授权。</li></ol> |
| 11 | 用户点击拒绝授权 | <ol><li>建议在需要获取用户信息前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。</li><li>可在 fail 回调中做引导授权，重新调用 my.getAuthCode 授权。</li></ol> |

# 常见问题

## Q：web-view 中如何进行用户授权？
A：web-view 中不支持调用 my.getAuthCode 接口。如果要在 web-view 中获取用户信息，请在小程序上下文中获取后传递到 web-view 中，可查看 [小程序与web-view内嵌H5相互通信](https://opendocs.alipay.com/support/01rb22)

## Q：如何同时进行用户基础信息、手机号、证件等授权（聚合授权）？
A：alipay.user.info.share 接口的每个用户信息字段（如：用户姓名，手机号码，生日等）需要单独申请开通，开通权限的字段会聚合展示在授权浮窗，可查看 [用户信息申请流程](https://opendocs.alipay.com/support/01rayg)。

## Q：调用 my.getAuthCode 获取到的 authCode 值是否每个用户是唯一的呢？
A：每次调用 my.getAuthCode 获取到的 authCode 值是不一样的，但是在同一个支付宝账号登录的情况下，根据此值获取到的 user_id 是唯一的。

更多常见问题可查看 [用户授权 FAQ](https://opendocs.alipay.com/mini/api/bpubha) 。
