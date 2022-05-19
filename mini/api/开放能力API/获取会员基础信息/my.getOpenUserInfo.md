
# 简介
**my.getOpenUserInfo** 是获取支付宝会员的基础信息（头像图片地址、昵称）的 API。

获取支付宝会员基础信息需要用户进行授权。授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的点击来触发。将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，当用户点击并同意之后，可以通过`my.getOpenUserInfo` 接口获取到支付宝会员的基础信息。

添加 [获取会员基础信息](https://opendocs.alipay.com/mini/introduce/twn8vq) 能力后才可以调用该接口。<br />


## 使用限制
- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。<br />
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。<br />

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/examples/c3ef65d4-5186-4eb6-aab9-95d6e59c800d) 

### .js 示例代码
唤起授权框，推荐兼容方案如下：
```html
<!-- .axml -->
<button a:if="{{canIUseAuthButton}}" open-type="getAuthorize" 
onGetAuthorize="onGetAuthorize" onError="onAuthError" 
scope='userInfo'>
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
success 回调函数会携带一个 Object 类型的对象，属性被解析后如下表所示：<br />**说明**：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| avatar | String | 头像图片地址。 |
| nickName | String | 昵称。 |
| gender | - | 强制返回空值 |
| countryCode | - | 强制返回空值 |
| province | - | 强制返回空值 |
| city | - | 强制返回空值 |

# 常见问题 FAQ
### Q：调用 my.getOpenUserInfo，报错“无效的授权关系”，如何处理？
A：用户 **主动授权** 后调用`my.getOpenUserInfo` 才能获取用户支付宝会员的基础信息。授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发操作。需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设为 `userinfo` ，示例代码如下：
```html
<!-- .axml -->
<button a:if="{{canIUseAuthButton}}" open-type="getAuthorize" 
onGetAuthorize="onGetAuthorize" onError="onAuthError" 
scope='userInfo'>
    会员基础信息授权
</button>
```

### Q：调用 my.getOpenUserInfo，报错 "ISV权限不足"，如何处理？
A：“获取会员信息”功能包已下架，若之前创建的应用已添加了“获取会员信息”的功能包则能正常调用接口，未添加的则无法再添加此功能。 新创建的应用请使用 [获取会员基础信息](https://opendocs.alipay.com/mini/introduce/twn8vq) my.getOpenUserInfo 接口。

1. 在小程序开发管理后台的 **功能列表** 中，点击 **添加功能**。

![|712x101](https://gw.alipayobjects.com/zos/skylark-tools/public/files/9219534cf0b476cb9654aa6dfcafcaff.png#align=left&display=inline&height=105&margin=%5Bobject%20Object%5D&originHeight=212&originWidth=1500&status=done&style=stroke&width=746)

2. 添加 **获取会员基础信息** 功能包。

![|712x369](https://gw.alipayobjects.com/zos/skylark-tools/public/files/f213001ed91e03d6fdd36a713f554f8e.png#align=left&display=inline&height=387&margin=%5Bobject%20Object%5D&originHeight=570&originWidth=1099&status=done&style=stroke&width=746)

### Q：“获取会员基础信息” 可以获取支付宝用户的 user_id 吗？
A：不可以。获取支付宝用户的 user_id 需要在服务端调用 [alipay.system.oauth.token](https://opendocs.alipay.com/mini/02qkj4)（换取授权访问令牌接口）。

更多问题请参阅 [获取会员基础信息 FAQ](https://opendocs.alipay.com/mini/api/qcn29g)<br />

### Q：“获取会员基础信息”可以获取用户身份证、真实姓名等信息吗？
A：不可以。“获取会员基础信息”只能获取用户头像、昵称信息。


