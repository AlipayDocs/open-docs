# 简介

**my.getAuthCode** 获取用户信息授权，取得授权码（authCode）。

my.getAuthCode 引导用户授权其信息给当前小程序，会弹出授权引导浮窗。请在用户充分了解小程序的业务内容后再调用 my.getAuthCode，避免损害用户体验；请勿在小程序首屏调用 my.getAuthCode，否则将面临违规处罚风险。

通过 my.getAuthCode 所取得的代表用户授权的授权码（authCode），后续需由小程序服务端使用，向支付宝换取实际信息（如 user_id、头像、昵称、手机号、地区、性别、出生日期等）。这种方式较通用，但也相对复杂（参见下文**接入必读**）。对于简单需求，建议优先选择其他方式：获取用户昵称和头像，请使用 [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh)；获取用户手机号，请使用 [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber)。

## 接入必读

通过 authCode 的方式获取用户信息，完整流程如下：

### 第一步：绑定产品

1. 到开放平台控制台为目标小程序绑定 [获取会员信息](https://open.alipay.com/develop/uni/mini/choose-product?bundleId=com.alipay.alipaywallet&productCode=I1080300001000042699) 产品。
2. 完成产品绑定以后，将看到 <a href="https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*XjlFSJPaySYAAAAAAAAAAAAAARQnAQ" target=_blank>用户信息申请</a>入口，点击进入第二步。如果看不到用户信息申请入口，则可能是账号权限不够，请联系当前小程序的应用管理员操作。

### 第二步：申请用户信息字段 

- 在 <a href="https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*LqsXR45_a4IAAAAAAAAAAAAAARQnAQ">用户信息申请</a> 页面，按需申请相应的字段。
- 每个字段的类目要求和审批规则不同，请参考 [用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu) 中的 **商家申请用户信息** 章节。
- 应隐私政策要求，**对 cert_type、cert_no、person_cert_expiry_date 的申请将不再通过**。有特殊要求（如政务类）的小程序请联系合作的支付宝业务人员。

### 第三步：获取用户授权

1. 第二步的申请审批通过后，在小程序上调用 my.getAuthCode 获取用户授权。调用时有两种可选的 scope：  <br>`auth_base`：基本信息授权，直接取得 authCode，此 authCode 仅可用于换取用户的 user_id（以 2088 开头的 16 位数字）。<br>`auth_user`：会员信息授权，会出现授权引导浮窗，第二步申请通过的字段都会一次性向用户展示，用户同意以后小程序可获得 authCode。
2. 获取 authCode 以后，小程序通过 my.request 等方式将其传递给服务端。

### 第四步：获取用户信息

1. 服务端使用 authCode，调用 [alipay.system.oauth.token](https://opendocs.alipay.com/open/02xtla) 取得 user_id 和 token（授权令牌）。
2. 如果第三步中使用的 scope 包含 auth_user，则服务端继续使用所取得的 token 调用 [alipay.user.info.share](https://opendocs.alipay.com/open/02xtlb) 最终获得用户信息。

## 使用限制

- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 此 API 支持在小程序插件中使用，授权主体是宿主小程序。
- 此 API 不支持在 web-view 中使用。如果要在 web-view 中使用用户信息，可在小程序上下文中获取后通过 [my.postMessage](https://opendocs.alipay.com/mini/component/web-view#%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81_2) 传给 web-view。


## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/1cdfd0855a5b2beb9466386548165516.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)


# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/get-auth-code?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### 示例代码

```javascript
my.getAuthCode({
  scopes: 'auth_user',
  success: res => {
    my.alert({
      title: 'my.getAuthCode 调用成功',
      content: `授权码：${res.authCode}`,
    });
  },
  fail: res => {
    my.alert({
      title: 'my.getAuthCode 调用失败',
      content: JSON.stringify(res),
    });
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| scopes | String/Array | 否 | 授权类型。支持 auth_base、auth_user，参见下文 **scopes 说明**。默认值 auth_base |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### scopes 说明

一个 scope 表示开发者需要请求用户授权的权限范围。

| **scopes** | **含义** | **后续链路** |
| --- | --- | --- |
| auth_base | 授权获取支付宝会员唯一标识（user_id）。此方式为静默授权，不会弹出授权浮窗。| 将小程序获取的 auth_code 传入服务端，调用 [alipay.system.oauth.token](https://opendocs.alipay.com/open/02xtla) 以获取支付宝会员唯一标识（user_id）。 |
| auth_user | 授权获取支付宝会员信息。| 将小程序获取的 auth_code 传入服务端，调用 [alipay.system.oauth.token](https://opendocs.alipay.com/open/02xtla)（换取授权访问令牌接口）换取授权访问令牌，然后调用 [alipay.user.info.share](https://opendocs.alipay.com/open/02xtlb) （支付宝会员授权信息查询接口）获取用户已授权的信息。 |

## 出参

success 回调函数会收到一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| authCode | String | 授权码。 |
| authErrorScopes | Object | 失败的授权类型，key 是授权失败的 scope，value 是对应的错误码。 |
| authSuccessScopes | Array | 成功的授权 scope。 |

## 错误码

fail 回调函数会收到一个 Object 类型的对象，其 error 字段为错误码，errorMessage 为错误信息：

| **错误码** | **错误信息** | **解决方案** |
| --- | --- | --- |
| 11 | 用户取消授权 | 充分说明获取用户信息的用途和必要性，重新引导操作。</li></ol> |
| 3 | 未找到授权结果 | 1、scopes 入参包含无效值（界面上会先会先弹出 <b>服务正忙，请稍后再试</b>），请检查 scopes 参数。2，Android 用户使用 back 键直接关闭了授权浮窗，请与 11 等同对待。 |
| 12 | Network Error | 授权相关网络请求失败或超时，请稍后重试。 |


# 常见问题

## Q：如何在一个弹窗里同时进行用户信息、手机号、身份证等授权？

A：参照上文 **接入必读** 部分第二步，成功申请的字段会在 my.getAuthCode 调用的弹窗里一次性授权。

## Q：调用 [alipay.user.info.share](https://opendocs.alipay.com/open/02xtlb) 获取用户已授权的信息时，报错 “isv 权限不足” 如何处理？

A：参照上文 **接入必读** 部分第一步和第二步，确保已经完成产品绑定和用户信息字段申请。

## Q：授权码（auth_code）无效应该如何处理（isv.code-invalid）？

A：授权码无效可能是以下几种情况，请对照排查。

- appId 选择错误

  请确认是否使用了正确的 appId。授权码必须是获取用户信息的商户进行调用。

  1. 如果是自调用模式，拼接授权链接的 appId 或者绑定小程序的 appId 必须与调用接口的 appId 一致。
  2. 如果是三方代调用模式（服务商代商户获取用户信息），在用户信息授权链接中 appId 必须设置为授权商户的 appId，而不是服务商的 appId。

- 授权码已被使用

  授权码一次有效，不可重复使用，请确定传入的授权码是否已经被使用过。

- 授权码过期

  授权码有期为 3 分钟到到 24 小时，超过有效期的授权码即使未使用也将自动失效。请检查传入的授权码是否因为长时间未使用已经过期。

## Q：web-view 中如何进行用户授权？

A：web-view 中不支持调用 my.getAuthCode 接口。如果要在 web-view 中使用用户信息，请在小程序上下文中获取后传递到 web-view 中。示例代码如下：

```javascript
// 小程序示例代码
const webviewContext = my.createWebViewContext('web-view-1');
my.getAuthCode({
  scopes: 'auth_user',
  success: res => {
    const authCode = res.authCode;
    // 在服务端获取用户信息
    my.request({
      // 你的服务器地址
      url: 'https://yourserveraddress',
      data: {
        authCode,
      },
      success(res) {
        // 获取需要的用户信息
        webviewContext.postMessage({
          data: res.data,
        });
      },
    });
  },
});

// web-view H5 示例代码
my.onMessage = function (message) {
  // 接受小程序发过来的用户信息
  console.log(message);
};
```
