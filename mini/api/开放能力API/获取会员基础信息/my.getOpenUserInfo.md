# 简介
**my.getOpenUserInfo** 是获取支付宝会员的基础信息的 API。

自 2022-06-13 [用户信息相关接口调整](https://forum.alipay.com/mini-app/post/73101020) 以后，此接口仅返回头像地址和昵称。

根据《中华人民共和国个人信息保护法》，为进一步规范开发者的用户个人信息处理行为，保障用户合法权益，支付宝小程序无论是通过调用支付宝官方提供的涉及用户个人信息的相关接口，还是开发者自行收集用户个人信息，均需补充相应的小程序隐私政策。详情可查看 [小程序隐私政策](https://opendocs.alipay.com/mini/03lwro)。

调用此 API 前需登录 [开放平台控制台](https://openhome.alipay.com/develop/manage) > 点击小程序，进入小程序详情页 > **开发** > **产品绑定** > **绑定产品**，选择绑定 **获取会员基础信息**。

获取支付宝会员基础信息需要用户进行授权，授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发， `<button>` 组件 `open-type` 的值设置为 `getAuthorize` 并将 `scope` 设为 `userInfo`。用户点击并同意之后，可以通过 `my.getOpenUserInfo` 接口获取到支付宝会员的基础信息。

## 使用限制
- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/get-user-info?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

### .js 示例代码
唤起授权框，推荐兼容方案如下：
```html
<!-- .axml -->
<button
  a:if="{{canIUseAuthButton}}"
  open-type="getAuthorize" 
  onGetAuthorize="onGetAuthorize"
  onError="onAuthError" 
  scope='userInfo'
>
  会员基础信息授权
</button>
```

#### 获取用户基础信息
用户点击同意后，即可通过 `my.getOpenUserInfo()` 获取用户基础信息：
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
可以通过以下方式获取用户信息中的某个参数。<br />以获取用户信息中的昵称为例：`console.log(JSON.parse(res.response).response.nickName)`

## 返回示例

### 返回 res 报文格式

- 成功返回 res 报文格式示例如下：<br />
```json
{"response": "{"response": {"code": "10000","msg": "Success","gender":"","countryCode":"","province":"","city":"","nickName": "XXX","avatar": "https://tfs.alipayobjects.com/images/partner/XXXXXXXX"}}"}
```

- 用户未授权获取会员基础信息，返回 res 报文格式示例如下：<br />
```json
{"response":"{"response":{"code":"40003","msg":"Insufficient Conditions","subCode":"isv.invalid-auth-relations","subMsg":"无效的授权关系"}}"}
```

## Button 属性说明
| **属性** | **说明** |
| --- | --- |
| open-type | getAuthorize 为授权组件（固定值）。 |
| scope | userInfo（固定值）。 |
| onGetAuthorize | 授权成功回调（在回调里可以调用获取信息的接口）。 |
| onError | 授权失败回调（包括用户拒绝和系统异常）。 |

## 入参
| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success  | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success
success 回调函数会携带一个 Object 类型的对象，属性被解析后如下表所示：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| avatar | String | 头像图片地址。 |
| nickName | String | 昵称。 |
| city | String | 历史遗留字段，恒为""。 |
| countryCode | String | 历史遗留字段，恒为""。 |
| province | String | 历史遗留字段，恒为""。 |
| gender | String | 历史遗留字段，恒为""。 |

# 常见问题 FAQ
## Q：调用 my.getOpenUserInfo，报错“无效的授权关系”，如何处理？
A：用户 **主动授权** 后调用`my.getOpenUserInfo` 才能获取用户支付宝会员的基础信息。授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发操作，需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设为 `userinfo`。

## Q：调用 my.getOpenUserInfo，报错 "ISV 权限不足"，如何处理？
A：调用此 API 需要绑定 **获取会员基础信息** 产品。登录 [开放平台控制台](https://openhome.alipay.com/develop/manage) > 点击小程序，进入小程序详情页 > **开发** > **产品绑定** > **绑定产品**，选择绑定 **获取会员基础信息**。

## Q：“获取会员基础信息” 可以获取支付宝用户的 user_id 吗？
A：不可以。获取支付宝用户的 user_id 需要在服务端调用 alipay.system.oauth.token（换取授权访问令牌接口）。

## Q：“获取会员基础信息” 可以获取用户身份证、真实姓名等信息吗？
A：不可以。“获取会员基础信息”只能获取用户头像、昵称信息。

更多问题请参阅 [获取会员基础信息 FAQ](https://opendocs.alipay.com/mini/api/qcn29g)
