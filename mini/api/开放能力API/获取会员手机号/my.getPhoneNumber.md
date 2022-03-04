
# 简介
**my.getPhoneNumber** 是获取支付宝用户绑定的手机号的 API。因为需要用户主动触发才能发起获取手机号，所以该功能不由 API 直接调用，必须点击 [button 组件](https://opendocs.alipay.com/mini/component/button) 来触发。

相关问题请参见 [获取会员手机号 FAQ](https://opendocs.alipay.com/mini/006lmr)。

有关获取会员手机号更多信息，请参见 [获取会员手机号](https://opendocs.alipay.com/mini/introduce/getphonenumber)。

## 使用限制

- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 目前该功能需要在开发者后台完成敏感信息申请才可以使用此功能，入口为 **开发管理** > **功能列表** > **添加功能** > **获取会员手机号** > **用户信息申请**，此功能需谨慎使用，若支付宝发现信息存在超出约定范围使用或者不合理使用等情况，支付宝有权永久回收该小程序的该接口权限。
- 需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，当用户点击并同意之后，可以通过 `my.getPhoneNumber()` 接口获取到支付宝服务器返回的加密数据， 然后在第三方服务端结合签名算法和 AES 密钥进行解密获取手机号，方法详见 [敏感信息加解密方法](https://opendocs.alipay.com/mini/2019110100244259)，若用户未授权，直接调用 `my.getPhoneNumber()` 接口，则无法返回正确信息。
- 因该 JSAPI 涉及获取用户隐私信息，使用该 JSAPI 前，请对照以下文档检查应用是否符合主营行业及字段使用场景的要求：[用户信息申请及使用基础规则](https://opendocs.alipay.com/mini/introduce/01sxqf)。

# 接口调用

## 示例代码
唤起授权框，推荐兼容方案。
```html
<button a:if="{{canIUseAuthButton}}" open-type="getAuthorize"
        onGetAuthorize="onGetAuthorize" onError="onAuthError" scope='phoneNumber'>
    授权手机号
</button>
```

### Button 属性说明
| **属性** | **描述** |
| --- | --- |
| open-type | getAuthorize 为授权组件。 |
| scope | phoneNumber。 |
| onGetAuthorize | 授权成功回调（在回调里可以调用获取信息的接口）。 |
| onError | 授权失败回调（包括用户拒绝和系统异常）。 |

用户点击同意后，即可通过my.getPhoneNumber()获取用户绑定的手机号。
```javascript
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

## 入参

Object 属性，参数如下：

| **属性** | **类型** | **必填** | **描述** |
| ---- | ---- | ---- | ---- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调会携带一个 Object 类型的对象 `res`，其参数如下：

| **属性** | **类型** | **描述** |
| ---- | ---- | ---- |
| response | String | 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理。 |

## 返回结果
res.response 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理（详细的服务端处理流程参考 [敏感信息加解密方法](https://opendocs.alipay.com/mini/2019110100244259)），服务端解密后的明文示例如下：

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

## 故障排查
调用 my.getPhoneNumber 获取手机号报错时，请检查以下配置内容：

- 请检查小程序后台已添加 **获取会员手机号** 功能包，并已在 **隐私内容申请** 中 **申请手机号**（若在小程序后台看不到敏感信息申请的入口，请使用主账号登录）。申请路径为：**小程序后台** > **开发管理** > **功能列表添加功能** > **获取会员手机号** > **敏感信息申请**。
- 请确保小程序添加了 JSAPI 基础包 （否则会报无权限）。 
- 请确保前端 AXML 中按照 button 授权方式，先获取用户授权然后使用 my.getPhoneNumber 进行获取（否则会报无效的授权关系）。

```html
<button a:if="{{canIUseAuthButton}}" open-type="getAuthorize" onGetAuthorize="onGetAuthorize" onError="onAuthError" scope='phoneNumber'>    授权手机号</button>
```

- 请确保已在 **小程序后台** > **设置** > **开发设置** 中，设置 **支付宝公钥**，**aes 密钥** 和 **应用网关**，aes 相关信息可参见 [内容加密接入指引](https://opendocs.alipay.com/mini/2019110100244259)。(若缺失这三个设置，在调用 my.getPhoneNumber 时可能只返回 response 不会返回sign)。
> 应用网关用于接收支付宝异步通知，例如口碑开店中，需要配置此网关来接收 [开发者门店被动通知](https://opendocs.alipay.com/open/205/105251/#%E5%BC%80%E5%8F%91%E8%80%85%E9%97%A8%E5%BA%97%E8%A2%AB%E5%8A%A8%E9%80%9A%E7%9F%A5) 。且一个 APPID 只能配置一个对应的应用网关,应用网关以 https:// 或 http://开头。
> 详见 [应用环境配置说明](https://docs.open.alipay.com/200/105310/#s2)。

调用 my.getPhoneNumber 没有获取到手机号时，请检查以下配置内容：

一般情况下都是当前用户的支付宝账号没有绑定手机号所致，需要当前用户登录 [账号管理](https://custweb.alipay.com/account/index.htm)，绑定手机号。
