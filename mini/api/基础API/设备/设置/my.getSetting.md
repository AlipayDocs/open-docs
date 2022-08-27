# 简介

**my.getSetting** 获取用户对当前小程序的各种授权状态，对应小程序设置中的部分选项。

小程序调用设备或者隐私信息相关的 API（如 my.getLocation、my.chooseImage）时，支付宝会弹出授权提示框，由用户决定是否授权给当前小程序。在 API 调用过以后，相关权限的授权状态，用户可在小程序设置界面板中查看和更改，开发者则可通过 my.getSetting 获取。

这些需要授权的 API 的成功调用，除了需要用户在支付宝内授权给小程序外，也需要用户在系统级别开启对应权限并授权给支付宝。两种授权状态相互独立，前者可通过 my.getSetting 获取，后者则需通过 my.getSystemInfo 获取。

**小程序授权相关的逻辑**

在用户未对小程序授权的情况下，调用需要权限的 API，客户端会向用户弹出授权提示框：
- 如果用户同意，API 的主体逻辑将会执行，且后续该 API 调用时不会再弹出授权提示；
- 如果用户拒绝，将直接触发 API 的 fail 回调，错误码一般为 2001（目前未完全统一，请以具体 API 文档为准）；如果用户在拒绝时勾选了“保持以上选择不再询问”，则 fail 回调错误码为 2003，且后续对该 API 的调用将直接失败（错误码为 2002），直到用户在小程序设置中重新开启此项权限。

用户在小程序设置中关闭某项授权后，再次调用相应 API 也会重新弹出授权提示；用户从“我的小程序”中删除当前小程序，等效于在小程序设置中关闭 my.getSetting 所包含的所有授权项。

对于因用户未授权给小程序而导致 API 调用失败、影响小程序正常使用的情况，建议给予用户恰当的引导说明，并在必要时调用 my.openSetting 打开小程序设置界面以便用户开启相关授权。

**系统级权限相关的逻辑**

如果某个 API 所需的特定权限用户并未在系统中开启，或者未授权给支付宝，那么即使用户同意将该权限授权给当前小程序，API 的调用仍会失败。一般来说，小程序对该 API 的首次调用也会触支付宝向系统申请权限，用户会看到相应的授权提示或者引导界面；用户拒绝以后的重复 API 调用或者永久拒绝情况下的 API 调用，则可能直接触发 fail 回调（错误码请参考具体 API 文档），用户将不会自动获得提示。开发者可通过 my.getSystemInfo 提前查询系统级授权情况，以区分这两种情况；针对后一种情况，可根据 API 回调信息或者再次调用 getSystemInfo 获取详情（例如 locationEnabled 为 false 表示手机未开启定位，locationAuthorized 为 false 表示用户未授予定位权限给支付宝），并采取恰当处理（如通过调用 my.showAuthGuide 唤起授权引导）。

**小程序设置中的其他项**

my.getSetting 能够获取的授权状态的范围当前主要集中在设备权限和隐私相关（也包括部分用户信息授权，如收货地址、会员基顾信息、手机号等），参见后文 **scope 列表**。

小程序设置界面中有展示但暂不支持通过 my.getSetting 查询的项目：
* 消息管理：即消息订阅状态，请在服务端使用 alipay.open.app.messagetemplate.subscribe.query 查询；
* 用户信息：
  * 通过 my.getAuthCode 获取用户授权的部分（如支付宝账号、姓名等），不提供单独的查询接口，开发者在恰当的时机调用 my.getAuthCode 并在回调中进行相应处理即可，已授权状态下 my.getAuthCode 二次调用不会再有弹框；
  * 其他项目（如刷脸认证等）授权状态，请参考相关的产品接入文档。


## 使用限制

- 基础库 [1.8.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.10 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
my.getSetting({
  success: res => {
    const { album = false, location = false } = res.authSetting;
    my.alert({ content: `相册已授权：${album}；地理位置已授权：${location}` });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| authSetting | Object | 用户授权结果，其中 key 为 scope 值，value 为 Boolean 值，表示用户是否允许授权，可查看 **scope 列表**。 |

### scope 列表

| **scope** | **对应接口** | **描述** |
| --- | --- | --- |
| location | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 地理位置。 |
| album | [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage) | 相册（访问）。 |
| writePhotosAlbum | [my.saveImageToPhotosAlbum](https://opendocs.alipay.com/mini/api/media/image/my.saveImagetophotosalbum) | 相册（保存）。 |
| camera | [my.scan](https://opendocs.alipay.com/mini/api/scan) | 摄像头。 |
| alipaysports | [my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v) | 运动数据。 |
| phoneNumber | [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) | 手机号码。 |
| aliaddress | [my.getAddress](https://opendocs.alipay.com/mini/api/lymgfk) | 收货地址。 |
| userInfo | [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) | 会员基础信息（昵称和头像地址）。 |

# 常见问题 FAQ

## Q：使用 my.getSetting 查询到 album、location 授权为 true，调用 my.chooseImage、my.getLocation 为何仍因为权限问题而失败？

A：my.getSetting 获取的只是用户在支付宝内对小程序的授权，但在系统级别用户可能关闭了相关功能或者未对支付宝授权。请参考本文简介部分的相关描述和建议。

## Q：通过 my.getAuthCode 进行的授权状态，可以通过 my.getSetting 接口查询吗？

A：暂不支持。开发者在恰当的时机调用 my.getAuthCode 并在回调中进行相应处理即可。已授权状态下 my.getAuthCode 二次调用不会再有弹框。
