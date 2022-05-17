
# 简介
**my.getOpenUserInfo** 可获取支付宝会员的基础信息（头像图片地址、昵称），接入方法可查看 [获取会员基础信息介绍](https://opendocs.alipay.com/mini/introduce/twn8vq)。<br />如需获取支付宝会员标识（user_id），请调用 [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize) 和 [alipay.system.oauth.token](https://opendocs.alipay.com/mini/02qkj4)（换取授权访问令牌接口）。<br />相关问题可查看 [获取会员基础信息 FAQ](https://opendocs.alipay.com/mini/api/qcn29g)。

## 使用限制

- 本接口在 IDE 模拟器中返回的数据为虚拟数据，真实数据请以真机调试效果为准。<br />
- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。<br />
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。<br />
- 本功能需要用户主动触发才能激活，所以该功能不由 API 直接调用，需用 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的点击来触发。将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，当用户点击并同意之后，可以通过`my.getOpenUserInfo` 接口获取到支付宝服务器返回的基础信息，若用户未授权，直接调用`my.getOpenUserInfo` 接口，则无法返回正确信息。<br />
- 需添加 **获取会员基础信息** 功能后，才可调用此接口。<br />
- 不能通过 `my.getOpenUserInfo` 接口获取支付宝会员标识（user_id）。<br />

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

- 未接入“获取用户基础信息”的功能包，返回 res 报文格式示例如下：<br />
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


## Function success
success 回调函数会携带一个 Object 类型的对象，属性被解析后如下表所示：<br />**说明**：

- 在 IDE 0.70 或以上的版本支持返回全部参数，avatar 和 nickName 是当前登录 IDE 用户的真实值，在真机上显示为真实值。<br />
- 若用户未设置 avatar 和 nickName，则不会返回这两个参数。<br />
| **属性** | **类型** | **是否必填** | **描述** |
| --- | --- | --- | --- |
| avatar | String | 选填 | 头像图片地址。 |
| nickName | String | 选填 | 昵称。 |
| gender | - | - | 强制返回空值 |
| countryCode | - | - | 强制返回空值 |
| province | - | - | 强制返回空值 |
| city | - | - | 强制返回空值 |


## 相关文档

- [获取会员基础信息](https://opendocs.alipay.com/mini/introduce/twn8vq)<br />
- [获取会员基础信息 FAQ](https://opendocs.alipay.com/mini/api/qcn29g)<br />
