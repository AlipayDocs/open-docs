### Q：调用 my.getOpenUserInfo，报错“无效的授权关系”，如何处理？

A：用户 **主动授权** 后调用`my.getOpenUserInfo` 才能获取用户支付宝会员的基础信息。授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发操作。需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设为 `userinfo`，示例代码如下：

```html
<!-- .axml -->
<button
  a:if="{{canIUseAuthButton}}"
  open-type="getAuthorize"
  onGetAuthorize="onGetAuthorize"
  onError="onAuthError"
  scope="userInfo"
>
  会员基础信息授权
</button>
```

### Q：“获取会员信息”、“获取会员基础信息”两个产品有什么区别？

A：为提高小程序开发效率，获取会员信息已升级为 获取会员基础信息。

自 2019 年 5 月 25 日 起，已不再支持添加获取会员信息。已添加获取会员信息功能包的小程序，在使用获取会员基础信息之前，仍需添加获取会员基础信息。

### Q：调用 alipay.user.info.share 报错“ISV 权限不足”如何处理？

A：alipay.user.info.share 是 **获取会员信息** 中使用的 API。获取会员信息已于 2019 年 5 月 25 日升级，在此日期之前未开通 **获取会员信息** 产品的小程序无法再调用 alipay.user.info.share，请使用获取会员基础信息。

### Q：调用 my.getOpenUserInfo 报错 "ISV 权限不足"如何处理？

A：获取会员信息已下架，若之前创建的应用已添加了获取会员信息则能正常调用接口，未添加的则无法再添加此功能。 新创建的应用请使用 [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) 接口。
进入 [开放平台控制台](https://open.alipay.com/develop/manage) 的 对应小程序详情页 > **产品绑定** 绑定 **获取会员基础信息**。
![](https://cdn.nlark.com/yuque/0/2022/png/179989/1661932867345-356a598e-9622-4c6d-b796-cea01549d7d2.png)

### Q：为什么接入“获取会员基础信息”功能并调用成功后，在获取用户信息时获取不到用户的昵称？

A：部分支付宝用户没有设置昵称，故获取不到用户昵称。

### Q：“获取会员基础信息” 可以获取支付宝用户的 user_id 吗？

A：不可以。获取支付宝用户的 user_id 需要在服务端调用 [alipay.system.oauth.token](https://opendocs.alipay.com/mini/02qkj4)（换取授权访问令牌接口）。

### Q：“获取会员基础信息”可以获取用户身份证、真实姓名等信息吗？

A：不可以。“获取会员基础信息”只能获取用户头像、昵称信息。

### Q：小程序获取会员基础信息时弹出两次授权窗，如何处理？

A：正常获取会员基础信息仅需使用 [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) 即可，只涉及一次授权弹窗。在获取用户 user_id + 获取用户基础信息场景需要弹窗两次进行授权确认：一次是 [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize) 获取用户授权码的授权框， 另一次是 my.getOpenUserInfo 中获取用户基础信息的授权框。

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
