# 简介

需要重点强调该操作并且引导用户去点击的入口通过按钮表达。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/7e1b1df43443c8d65bbb3071d3e3211a.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)
# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/button/index&defaultOpenedFiles=pages/button/index&theme=light)

## 属性说明

| 属性     | 类型    | 描述 |
|----------|---------|------|
| size     | String  | 有效值 default, mini（小尺寸）。<br />默认值：default |
| type     | String  | 按钮的样式类型，有效值 primary、default、warn。<br />默认值：default |
| plain    | Boolean | 是否镂空（ghost 与 plain 等效）。<br />默认值：false |
| disabled | Boolean | 是否禁用。<br />默认值：false |
| loading  | Boolean | 按钮文字前是否带 loading 图标。<br />默认值：false |
| hover-class | String | 按钮按下去的样式类。`button-hover` 默认为 `{background-color: rgba(0, 0, 0, 0.1); opacity: 0.7;}，hover-class="none"` 时表示没有点击效果。<br />默认值：button-hover |
| hover-start-time | Number | 按住后多少时间后出现点击状态，单位毫秒。<br />默认值：20 |
| hover-stay-time | Number | 手指松开后点击状态保留时间，单位毫秒。<br />默认值：70 |
| hover-stop-propagation | Boolean | 是否阻止当前元素的祖先元素出现点击样式。<br />默认值：false<br />版本要求：基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| form-type | String | 有效值：submit、reset，用于 [form 表单](https://opendocs.alipay.com/mini/component/form) 组件，点击分别会触发 submit/reset 事件。 |
| open-type | String | 开放能力。<br />版本要求：基础库 [1.1.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| scope | String | 当 open-type 为 getAuthorize 时有效。<br />版本要求：基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onTap | EventHandle | 点击。<br />说明：每点击一次会触发一次事件，建议自行使用代码防止重复点击，可以使用 js 防抖和节流实现。 |
| public-id | String | 生活号 id，必须是当前小程序同主体且已关联的生活号，`open-type="lifestyle"` 时有效。 |
| onGetAuthorize | EventHandle | 当 open-type 为 getAuthorize 时有效。<br />当授权成功时触发。<br />版本要求：基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onFollowLifestyle | EventHandle | 当 open-type 为 lifestyle 时有效。<br />当点击按钮时触发。<br />`event.detail = { followStatus }`，`followStatus` 合法值有 `1`、`2`、`3`，其中 `1` 表示已关注，`2` 表示用户不允许关注，`3` 表示发生未知错误；<br />已知问题：基础库 1.0，当用户在点击按钮前已关注生活号，`event.detail.followStatus` 的值为 `true`。<br />版本要求：基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onError | EventHandle | 当 open-type 为 getAuthorize 时有效。<br />当授权失败时触发。`event.detail = {type, errorMessage}`，此时 `type` 的值为 `getAuthorize`。<br />版本要求：基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onGetUserInfo | EventHandler | 当 open-type 为 getAuthorize 且 scope 为 userInfo 时有效。<br>当授权成功时触发。<br>版本要求：基础库 2.8.0 及以上。<br>event.detail：<br>&nbsp;&nbsp;&nbsp;&nbsp;userInfo：<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;avatar，头像<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nickName，昵称 |
| onGetPhoneNumber | EventHandler | 当 open-type 为 getAuthorize 且 scope 为 phoneNumber 时有效。<br>当授权成功时触发。<br>版本要求：基础库 2.8.0 及以上。<br>成功获取用户信息后返回<br>event.detail：<br>&nbsp;&nbsp;&nbsp;&nbsp;encryptedData，加密后的手机号<br>&nbsp;&nbsp;&nbsp;&nbsp;sign，签名信息，如果在开放平台后台配置了加签方式后有此字段 |

### open-type 有效值

| 属性        | 描述 |
|-------------|------|
| share       | 触发[自定义分享](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0)，可使用`my.canIUse`('button.open-type.share') 判断。<br />版本要求：基础库 [1.1.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| getAuthorize | 支持小程序授权，可使用 `my.canIUse`('button.open-type.getAuthorize')判断。<br />版本要求：基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| contactShare | 分享到通讯录好友，可使用 `my.canIUse`('button.open-type.contactShare')判断。<br />版本要求：基础库 **1.11.0** 及以上 |
| lifestyle    | [关注生活号](https://opendocs.alipay.com/mini/introduce/bntnry)，可使用 `my.canIUse`('button.open-type.lifestyle') 判断。<br />版本要求：基础库 **1.11.0** 及以上 |

### scope 有效值

当 open-type 为 getAuthorize 时，可以设置 scope 为以下值：

| 属性      | 描述 |
|-----------|------|
| phoneNumber | 用户点击同意后，即可通过 [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) 授权小程序获取用户绑定的手机号。<br />版本要求：基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| userInfo | 用户点击同意后，即可通过 [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) 授权小程序获取支付宝会员基础信息。<br />版本要求：基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
# 常见问题

### 使用 button 点击授权获取手机号，服务端要怎么解密？

请查看文档 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3) 。

### button 如何去除默认边框？

修改 style 属性为：`border: 0; padding: 0;`

### 如何实现自定义分享中的 button: 页面分享按钮触发？

通过给 button 组件设置属性 `open-type="share"`，可以在用户点击按钮后触发。
