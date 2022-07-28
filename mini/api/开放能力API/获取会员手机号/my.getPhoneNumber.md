# 简介
**my.getPhoneNumber** 是获取支付宝用户绑定的手机号的 API。

根据《中华人民共和国个人信息保护法》，为进一步规范开发者的用户个人信息处理行为，保障用户合法权益，支付宝小程序无论是通过调用支付宝官方提供的涉及用户个人信息的相关接口，还是开发者自行收集用户个人信息，均需补充相应的小程序隐私政策。详情可查看 [小程序隐私政策](https://opendocs.alipay.com/mini/03lwro)。

此 API 涉及获取用户隐私信息，使用此 API 前请对照以下文档检查应用是否符合主营行业及字段使用场景的要求：[用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu)。

此 API 会返回加密后的用户手机号，需要提前设置应用加密方式。在开放平台控制台 > 开发设置中配置 **接口内容加密方式**。详见 [接口内容加密方式]((https://opendocs.alipay.com/common/02mse3))。

如果需要验证加密内容的真实性，请确保已在小程序详情页完成 [接口加签方式](https://opendocs.alipay.com/common/02mriz) 设置。

调用此 API 需要绑定相关产品。登录 [开放平台控制台](https://openhome.alipay.com/develop/manage) > 点击小程序，进入小程序详情页 > **开发** > **产品绑定** > **绑定产品**，选择绑定 **获取会员手机号**。

获取支付宝会员手机号需要用户进行授权，授权行为通过 [<button> 组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发， `<button>` 组件 `open-type` 的值设置为 `getAuthorize` 并将 `scope` 设为 `phoneNumber`。用户点击并同意之后，可以通过 `my.getPhoneNumber` 接口获取到支付宝会员加密后的手机号。最后在服务端结合签名算法和 AES 密钥进行解密获取手机号，方法可查看 [接口内容加解密方式](https://opendocs.alipay.com/common/02mse3)。

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
onGetAuthorize(res) {
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
},
```

## 返回示例

res.response 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理，详细的服务端处理流程可查看 [接口内容加解密方式](https://opendocs.alipay.com/common/02mse3)，服务端解密后的明文示例如下：

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

## Q：调用 my.getPhoneNumber，报错 “无效的授权关系”，如何处理？
A：用户 **主动授权** 后调用`my.getPhoneNumber` 才能获取用户支付宝会员的手机号。授权行为通过 `<button>` 组件的 **点击** 动作来触发操作，需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设为 `phoneNumber`。

## Q：调用 my.getPhoneNumber，报错 “缺少加密配置”，如何处理？
A：请先在开放平台控制台 > 开发设置中配置 **接口内容加密方式**。详见 [接口内容加密方式]((https://opendocs.alipay.com/common/02mse3))。

## Q：调用 my.getPhoneNumber，报错 "ISV 权限不足"，该如何处理？
A：
- 调用此 API 需要绑定 **获取会员手机号** 产品。登录 [开放平台控制台](https://openhome.alipay.com/develop/manage) > 点击小程序，进入小程序详情页 > **开发** > **产品绑定** > **绑定产品**，选择绑定 **获取会员手机号**。

## Q：调用 my.getPhoneNumber，没有返回 sign 签名字段，该如何处理？
- 请确保已在小程序详情页完成 [接口加签方式](https://opendocs.alipay.com/common/02mriz) 设置。

## Q：为什么调用 my.getPhoneNumber 没有获取到手机号？
A：一般情况下都是当前用户的支付宝账号没有绑定手机号所致，需要当前用户登录 [账号管理](https://custweb.alipay.com/account/index.htm)，绑定手机号。

更多问题请查看 [获取会员手机号 FAQ](https://opendocs.alipay.com/mini/api/dwou7f)。
