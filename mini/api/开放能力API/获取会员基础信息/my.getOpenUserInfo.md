# 简介

**my.getOpenUserInfo** 是获取支付宝会员的基础信息的 API。

自 2022-06-13 [用户信息相关接口调整](https://forum.alipay.com/mini-app/post/73101020) 以后，此接口仅返回头像地址和昵称。

使用此 API 需绑定 **获取会员基础信息** 产品，操作步骤如下。登录 [开放平台控制台](https://openhome.alipay.com/develop/manage) > 点击小程序，进入小程序详情页 > **开发** > **产品绑定** > **绑定产品**，选择绑定 **获取会员基础信息**。未绑定 **获取会员基础信息** 产品直接调用此 API 会返回

```json
{
  "code": "40006",
  "msg": "Insufficient Permissions",
  "subCode": "isv.insufficient-isv-permissions",
  "subMsg": "ISV权限不足，建议在开发者中心检查对应功能是否已经添加，解决办法详见：https://docs.open.alipay.com/common/isverror"
}
```

获取支付宝会员基础信息需要用户进行授权。授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发。将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize` 并将 `scope` 设为 `userInfo`。用户点击并同意之后，可以通过 `my.getOpenUserInfo` 接口获取到支付宝会员的基础信息。未经过 Button 授权直接调用此 API 会返回

```json
{
  "code": "40003",
  "msg": "Insufficient Conditions",
  "subCode": "isv.invalid-auth-relations",
  "subMsg": "无效的授权关系"
}
```

## 使用限制

- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/get-user-info?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发。

唤起授权框，推荐兼容方案如下：

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

#### 获取用户基础信息

用户点击同意后，即可通过 `my.getOpenUserInfo()` 获取用户基础信息：

```javascript
// .js
data: {
  canIUseAuthButton: my.canIUse('button.open-type.getAuthorize')
},
onGetAuthorize(res) {
  my.getOpenUserInfo({
    fail: (res) => {
    },
    success: (res) => {
      let userInfo = JSON.parse(res.response).response // 以下方的报文格式解析两层 response
    }
  });
},
```

## 返回示例

### 返回 res 报文格式

- 成功返回 res 报文格式示例如下：<br />

```js
{
  response: '{"response": {"code": "10000","msg": "Success","gender":"","countryCode":"","province":"","city":"","nickName": "XXX","avatar": "https://tfs.alipayobjects.com/images/partner/XXXXXXXX"}}';
}
```

- 未绑定获取会员基础信息产品，返回 res 报文格式示例如下：<br />

```js
{
  response: '{"response":{"code":"40006","msg":"Insufficient Pe…tps:\\/\\/docs.open.alipay.com\\/common\\/isverror"}}';
}
```

- 用户未授权获取会员基础信息，返回 res 报文格式示例如下：<br />

```js
{
  response: '{"response":{"code":"40003","msg":"Insufficient Co…"isv.invalid-auth-relations","subMsg":"无效的授权关系"}}';
}
```

## 入参

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，属性被解析后如下表所示：

| **属性**    | **类型** | **描述**               |
| ----------- | -------- | ---------------------- |
| avatar      | String   | 头像图片地址。         |
| nickName    | String   | 昵称。                 |
| city        | String   | 历史遗留字段，恒为""。 |
| countryCode | String   | 历史遗留字段，恒为""。 |
| province    | String   | 历史遗留字段，恒为""。 |
| gender      | String   | 历史遗留字段，恒为""。 |

# 常见问题 FAQ

## Q：调用 my.getOpenUserInfo，报错“无效的授权关系”，如何处理？

A：

- 用户 **主动授权** 后调用`my.getOpenUserInfo` 才能获取用户支付宝会员的基础信息。授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发操作，需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设为 `userInfo`。
- 可以通过 [my.getSetting](https://opendocs.alipay.com/mini/api/xmk3ml) 接口返回的 userInfo 字段判断用户是否授权过会员基础信息，userInfo 为 true 即已授权。

## Q：调用 my.getOpenUserInfo，报错 "ISV 权限不足"，如何处理？

A：“获取会员信息”功能包已下架，若之前创建的应用已添加了“获取会员信息”的功能包则能正常调用接口，未添加的则无法再添加此功能。

1. 在小程序开发管理后台的 **产品绑定** 中，点击 **绑定产品**。

![|712x101](https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*XL89TIDxbVoAAAAAAAAAAAAAARQnAQ)

2. 绑定 **获取会员基础信息** 产品。

![|712x369](https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*WaCESJQ8cBwAAAAAAAAAAAAAARQnAQ)

## Q：如何获取除用户头像、昵称信息以外的用户信息？

A：**获取会员基础信息** 只支持获取用户头像、昵称信息。如果需要获取其他用户信息，参阅 [用户信息申请流程](https://opendocs.alipay.com/common/02kkuu)

## Q：为什么调用 my.getOpenUserInfo 返回的用户的昵称为空？

A：部分支付宝用户没有设置昵称，故获取不到用户昵称。
