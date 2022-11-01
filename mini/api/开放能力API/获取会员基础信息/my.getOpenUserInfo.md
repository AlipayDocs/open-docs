# 简介

**my.getOpenUserInfo** 是获取支付宝会员基础信息（头像地址和昵称）的 API。

# 接入必读

1、请到平台控制台为当前小程序绑定 [获取会员基础信息](https://open.alipay.com/develop/uni/mini/choose-product?bundleId=com.alipay.alipaywallet&productCode=I1080300001000054282) 产品。**未绑定该产品而直接调用此 API，会收到报错“ISV权限不足”（code 40006）**。

2、请参考示例代码，使用 open-type 为 getAuthorize、scope 为 userInfo 的 [`<button>` 组件](https://opendocs.alipay.com/mini/component/button)，由用户触发并完成授权，再在 onGetAuthorize 回调函数中调用 my.getOpenUserInfo()，用户拒绝授权事件在 <button> 组件监听 onError 回调。**未经用户授权而直接调用此 API，会收到报错“无效的授权关系”（code 40003）**。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/get-user-info?view=preview&defaultPage=pages/base-info/base-info&defaultOpenedFiles=pages/base-info/base-info&theme=light&priority=js)

### .axml 示例

```html
<button
  open-type="getAuthorize"
  scope="userInfo"
  onGetAuthorize="getOpenUserInfo"
  onError="handleAuthError"
>
  会员基础信息授权
</button>
```

### .js 示例
```javascript
Page({
  getOpenUserInfo() {
    my.getOpenUserInfo({
      success: (res) => {
        const { code, subMsg, avatar, nickName,  } = JSON.parse(res.response).response;
        if (code == '10000') {
          my.alert({
            title: 'getOpenUserInfo success',
            content: JSON.stringify({ avatar, nickName }),
          });  
        } else {
          if (code == '40006') {
            // 请参考接入必读，到小程序控制台绑定产品
          }
          my.alert({
            title: 'getOpenUserInfo fail',
            content: JSON.stringify({ code, subMsg }),
          });
        }
      },
      fail: (res) => {
        my.alert({
          title: 'getOpenUserInfo fail',
          content: JSON.stringify(res),
        }); 
      },
    });
  },
  handleAuthError(e) {
    my.alert({ title: '用户拒绝授权', content: JSON.stringify(e.detail) });
  }
});
```

## 入参

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 出参

success 回调函数会携带一个 Object 类型的对象 res。使用 JSON.parse(res.response).response 解析，所得对象的有效字段如下：

| **属性**    | **类型** | **描述**               |
| ----------- | -------- | ---------------------- |
| code        | String   | 结果码。10000 为成功，其他情况为失败。40003 和 40006 是较为常见的报错，请参考上文**接入必读**。|
| subMsg      | String   | 结果消息。 |
| avatar      | String   | 会员头像图片地址。 |
| nickName    | String   | 会员昵称。 |


# 常见问题

## Q：调用 my.getOpenUserInfo，报错 "ISV 权限不足"，如何处理？

A：需要先在开放平台控制台绑定产品，参见上文**接入必读** 1。

## Q：调用 my.getOpenUserInfo，报错“无效的授权关系”，如何处理？

A：成功调用 my.getOpenUserInfo 须经过用户授权，参见上文**接入必读** 2。可通过 [my.getSetting](https://opendocs.alipay.com/mini/api/xmk3ml) 接口返回的 userInfo 字段判断用户是否授权过会员基础信息，userInfo 为 true 即已授权。

## Q：如何获取除用户头像、昵称信息以外的用户信息？

A：my.getOpenUserInfo 只支持获取用户头像和昵称信息。如需获取用户其他信息，请参阅 [用户信息申请流程](https://opendocs.alipay.com/common/02kkuu)。

## Q：为什么调用 my.getOpenUserInfo 返回的用户的昵称为空？

A：部分支付宝用户没有设置昵称，故获取不到用户昵称。
