### Q：小程序如何实现用户授权？

A：小程序不支持使用拼接授权链接进行授权，建议使用 [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize) 实现用户授权、用户登录等。

### Q：先调用 my.getAuthCode，再调用 my.getOpenUserInfo 会出现两次授权窗口，是否有方法可以实现只出现一个授权弹框？

A：正常获取会员基础信息是需要弹窗两次进行授权确认的，一次是 my.getAuthCode 获取用户授权码的授权框， 一次是 my.getOpenUserInfo 中获取用户基础信息的授权框。

my.getAuthCode 使用静默授权方法（令 scopes 为 auth_base）即可实现只出现一个授权弹框。示例代码如下：

```javascript
my.getAuthCode({
  scopes: ['auth_base'],
  success: res => {
    my.alert({
      content: res.authCode,
    });
  },
});
```

### Q：如何打印 my.getAuthCode 获取到的 authCode？

A：在 IDE 中使用 console.log，在 console 里打印即可。示例代码如下：

```javascript
my.getAuthCode({
  scopes: 'auth_user',
  success: res => {
    console.log(res.authCode),
      my.alert({
        content: res.authCode,
      });
  },
});
```

效果如下图所示：

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/6154e61a1f0d1387f5ec0da08926a267.png?x-oss-process=image/resize,w_1500#align=left&display=inline&height=394&margin=%5Bobject%20Object%5D&originHeight=793&originWidth=1500&status=done&style=none&width=746)

### Q：为什么要使用用户授权 my.getAuthCode API?

A：开发者在支付宝开放平台上读写用户信息，均需经过用户许可。支付宝开放平台的用户授权基于国际标准的 OAuth2.0 授权机制。基于此机制，使用 my.getAuthCode API 得到用户授权后，方可进行获取用户信息、给用户发放会员卡等操作。

### Q：为什么不允许在小程序首屏使用用户授权 API？

A：为了创造更良好的支付宝小程序用户体验，在小程序的首屏引导用户授权是不被允许的。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。

### Q：用户的 user_id 可以通过用户授权 API 获取吗？

A：不可以，user_id 需要绑定 **获取会员基础信息** 获取。

### Q：my.getAuthCode 可以在小程序 onload 的时候用吗？

A：可以，但是必须是静默授权。小程序审核禁止一进入就强制弹授权框。

### Q：my.getAuthCode 获取用户信息和手机号，为何报 isv.insufficient-isv-permissions？

A：

- 报错描述：ISV 权限不足，建议在控制台检查对应功能是否已经添加。
- 报错原因：此报错的含义就是没有对应接口权限。
- 解决方案：
  - 配置的账号是否有当前接口权限或代理的商家是否有当前接口权限。<br />可查看 [如何确认是否完成开通](https://opendocs.alipay.com/support/01raue)。若没有请先完成开通，开通相关问题可咨询商服服务热线 4007585858。
  - 是否在对应 APPID 中的隐私申请下申请了获取会员信息功能，每个字段的类目要求和审批规则不同，请参考 [隐私申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu#%E5%95%86%E5%AE%B6%E7%94%B3%E8%AF%B7%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)。
  - 若是服务商，检查授权令牌（app_auth_token）是否有对应的接口权限。
  - 如在沙箱调试出现，请确认请求网关为沙箱 OpenAPI 网关 `https://openapi.alipaydev.com/gateway.do`，并且请求的 app_id 为沙箱的 app_id。
  - 检查此 APPID 是否已经上线，目前必须上线的应用才可以在正式环境调用接口。

### Q：调用 my.getAuthCode 获取到的 authCode 值是否每个用户是唯一的呢？

A：调用 my.getAuthCode 获取到的 authCode 值是不一样的，但是在同一个支付宝账号登录的情况下，根据此值获取到的 user_id 是唯一的。
