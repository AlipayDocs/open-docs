
### Q1：调用 my.getOpenUserInfo，报错“无效的授权关系”，如何处理？
A：用户 **主动触发** 才能发起获取会员基础信息请求，不能由 API 直接获取会员基础信息，需使用 [button 组件](/mini/component/button) 的“点击”动作来触发操作。需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设为 `userinfo` ，示例代码如下：
```html
<!-- .axml -->
<button a:if="{{canIUseAuthButton}}" open-type="getAuthorize" 
onGetAuthorize="onGetAuthorize" onError="onAuthError" 
scope='userInfo'>
    会员基础信息授权
</button>
```

### Q2：“获取会员信息”、“获取会员基础信息”两个功能包有什么区别？
A：为提高小程序开发效率，“获取会员信息”功能包已升级为“[获取会员基础信息](/mini/introduce/twn8vq)” 功能包。

自 2019 年 5 月 25 日 起，已不再支持添加“获取会员信息”功能包。

已添加“获取会员信息”功能包的小程序，在使用“获取会员基础信息”功能之前，仍需添加“获取会员基础信息”功能包。

### Q3：调用 alipay.user.info.share 报错“ISV 权限不足”如何处理？
A：alipay.user.info.share 是“获取会员信息”功能包中使用的 API。“获取会员信息”功能包已于2019 年5月25日升级，在此日期之前未签约“获取会员信息”功能包的小程序无法再调用 alipay.user.info.share，请使用“[获取会员基础信息](/mini/introduce/twn8vq)”功能包。

### Q4：调用 my.getOpenUserInfo 报错 "ISV权限不足"如何处理？
A：“获取会员信息”功能包已下架，若之前创建的应用已添加了“获取会员信息”的功能包则能正常调用接口，未添加的则无法再添加此功能。 新创建的应用请使用 [获取会员基础信息](/mini/introduce/twn8vq) my.getOpenUserInfo 接口。

1. 在小程序开发管理后台的 **功能列表** 中，点击 **添加功能**。

![|712x101](https://gw.alipayobjects.com/zos/skylark-tools/public/files/9219534cf0b476cb9654aa6dfcafcaff.png#align=left&display=inline&height=105&margin=%5Bobject%20Object%5D&originHeight=212&originWidth=1500&status=done&style=stroke&width=746)

2. 添加 **获取会员基础信息** 功能包。

![|712x369](https://gw.alipayobjects.com/zos/skylark-tools/public/files/f213001ed91e03d6fdd36a713f554f8e.png#align=left&display=inline&height=387&margin=%5Bobject%20Object%5D&originHeight=570&originWidth=1099&status=done&style=stroke&width=746)

### Q5：为什么接入“获取会员基础信息”功能并调用成功后，在获取用户信息时获取不到用户的昵称？
A：部分支付宝用户没有设置昵称，故获取不到用户昵称。

### Q6：小程序可以同时获取手机号、头像、昵称等公开信息吗?
A：不能在同一个弹框中同时获取会员手机号和头像、昵称。

可分别获取会员手机号，和获取用户头像及昵称。

详情请参见：

- [获取会员手机号](/mini/introduce/getphonenumber)
- [获取会员基础信息](/mini/introduce/twn8vq)（获取头像、昵称、性别、所在地区等信息）

### Q7：“获取会员基础信息” 可以获取支付宝用户的 user_id 吗？
A：不可以。获取支付宝用户的 user_id 需要在服务器端调用 [alipay.system.oauth.token](https://docs.open.alipay.com/api_9/alipay.system.oauth.token) 。

### Q8：“获取会员基础信息”可以获取用户身份证、真实姓名等信息吗？
A：不可以。“获取会员基础信息”只能获取用户头像、昵称、性别、所在地区等信息。

### Q9：小程序获取会员基础信息时弹出两次授权窗，如何处理？
A：正常获取会员基础信息仅需使用 [my.getOpenUserInfo](https://opendocs.alipay.com/mini/02otr4) 即可，只涉及一次授权弹窗。在获取用户 user_id + 获取用户基础信息场景需要弹窗两次进行授权确认：一次是 [my.getAuthCode](/mini/api/openapi-authorize) 获取用户授权码的授权框， 另一次是 my.getOpenUserInfo 中获取用户基础信息的授权框。

my.getAuthCode 使用静默授权方法（令 scopes 为 auth_base）即可实现只出现一个授权弹框。示例代码如下：
```javascript
my.getAuthCode({
  scopes: ['auth_base'],
  success: (res) => {
    my.alert({
      content: res.authCode,
    });
  },
});
```
