# 简介
**my.getPhoneNumber** 是获取支付宝用户绑定的手机号的 API。

此 API 涉及获取用户隐私信息，使用此 API 前请对照以下文档检查应用是否符合主营行业及字段使用场景的要求：[用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu)。

获取支付宝会员手机号需要用户进行授权，授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发， `<button>` 组件 `open-type` 的值设置为 `getAuthorize` 并将 `scope` 设为 `phoneNumber`。用户点击并同意之后，可以通过 `my.getPhoneNumber` 接口获取到支付宝会员加密后的手机号。最后在服务端结合签名算法和 AES 密钥进行解密获取手机号，方法可查看 [接口内容加解密方式](https://opendocs.alipay.com/common/02mse3)

目前该功能需要在开发者后台完成敏感信息申请后才可以使用，入口为 **开发管理** > **功能列表** > **添加功能** > **获取会员手机号** > **用户信息申请**，此功能需谨慎使用，若支付宝发现信息存在超出约定范围使用或者不合理使用等情况，支付宝有权永久回收该小程序的该接口权限。

更多信息请参阅 [获取会员手机号](https://opendocs.alipay.com/mini/introduce/getphonenumber)。

## 使用限制

- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码
唤起授权框，推荐兼容方案。
```html
<button
  a:if="{{canIUseAuthButton}}"
  open-type="getAuthorize"
  onGetAuthorize="onGetAuthorize"
  onError="onAuthError"
  scope='phoneNumber'
>
  授权手机号
</button>
```

### .js 示例代码
用户点击同意后，即可通过 my.getPhoneNumber() 获取用户绑定的手机号。
```javascript
data: {
  canIUseAuthButton: my.canIUse('button.open-type.getAuthorize')
},
my.getPhoneNumber({
  success: (res) => {
    let encryptedData = res.response;
    my.request({
      url: '你的后端服务端',
      data: encryptedData,
    });
  },
  fail: (res) => {
    console.log(res);
    console.log('getPhoneNumber_fail');
  },
});
```

## 返回示例

res.response 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理，详细的服务端处理流程可查看 方法可查看 [接口内容加解密方式](https://opendocs.alipay.com/common/02mse3)，服务端解密后的明文示例如下：

### 正常响应
```json
{
  "code": "10000",
  "msg": "Success",
  "mobile": "1597671905"
}
```

### 异常响应
```json
{
  "code": "40003",
  "msg": "Insufficient Conditions",
  "subCode": "isv.invalid-auth-relations",
  "subMsg": "无效的授权关系"
}
{
  "code": "20000",
  "msg": "Service Currently Unavailable",
  "subCode": "aop.unknow-error",
  "subMsg": "系统繁忙"
}
{
  "code": "40001",
  "msg": "Missing Required Arguments",
  "subCode": "isv.missing-default-signature-type",
  "subMsg": "应用未设置默认签名类型"
}
// 解决方案：重新保存下开发者的密钥，或者设置下小程序的应用网关地址
{
  "code": "40002",
  "msg": "Invalid Arguments",
  "subCode": "isv.invalid-encrypt",
  "subMsg": "加密异常"
}
// 解决方案：按文档重新设置AES密钥
```

## Button 属性说明
| **属性** | **描述** |
| --- | --- |
| open-type | getAuthorize 为授权组件。 |
| scope | phoneNumber。 |
| onGetAuthorize | 授权成功回调（在回调里可以调用获取信息的接口）。 |
| onError | 授权失败回调（包括用户拒绝和系统异常）。 |

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| ---- | ---- | ---- | ---- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调会携带一个 Object 类型的对象，其参数如下：

| **属性** | **类型** | **描述** |
| ---- | ---- | ---- |
| response | String | 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理。 |

# 常见问题 FAQ
### Q：调用 my.getPhoneNumber，报错“无效的授权关系”，如何处理？
A：用户 **主动授权** 后调用`my.getPhoneNumber` 才能获取用户支付宝会员的手机号。授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发操作，需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设为 `phoneNumber`。

### Q：调用 my.getPhoneNumber 获取手机号报错，该如何处理？
A：
- 请检查小程序已添加 **获取会员手机号** 功能包，并已在 **隐私内容申请** 中 **申请手机号**（若在小程序详情页看不到敏感信息申请的入口，请使用主账号登录）。申请路径为：[开放平台控制台](https://open.alipay.com/dev/workspace) > 选择需要配置的应用，点击进入应用详情页 > **管理** > **能力管理**，添加 **获取会员手机号** 能力 > **用户信息申请**。
- 请确保已在小程序详情页完成 [接口加签方式](https://opendocs.alipay.com/common/02mriz) 、[接口内容加密方式](https://opendocs.alipay.com/common/02mse3)、[应用网关](https://opendocs.alipay.com/common/02qibh) 设置，若缺失这三个设置，在调用 my.getPhoneNumber 时可能只返回 response 不会返回 sign。<br />应用网关用于接收支付宝异步通知，例如口碑开店中，需要配置此网关来接收开发者门店被动通知。且一个 APPID 只能配置一个对应的应用网关，应用网关以 https:// 或 http:// 开头。<br />

### Q：为什么调用 my.getPhoneNumber 没有获取到手机号？
A：一般情况下都是当前用户的支付宝账号没有绑定手机号所致，需要当前用户登录 [账号管理](https://custweb.alipay.com/account/index.htm)，绑定手机号。

更多问题请参阅 [获取会员手机号 FAQ](https://opendocs.alipay.com/mini/api/dwou7f)。
