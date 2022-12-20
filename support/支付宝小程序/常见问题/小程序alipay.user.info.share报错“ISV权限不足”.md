## 错误描述
小程序获取会员信息 alipay.user.info.share 报错“isv.insufficient-isv-permissions（ISV权限不足）”。
```html
{"code":"40006",
"msg":"Insufficient Permissions",
"sub_code":"isv.insufficient-isv-permissions",
"sub_msg":"ISV权限不足"}
```

## 问题原因

- 支付宝网关设置错误。
- 小程序不支持调用 alipay.user.info.share。 

## 解决方案

### 支付宝网关设置错误
检查支付宝网关是否正确：

- 生产环境（OpenAPI网关）：https://openapi.alipay.com/gateway.do。
- 沙箱环境（沙箱网关）：https://openapi.alipaydev.com/gateway.do。

### 不支持alipay.user.info.share
alipay.user.info.share 是 **获取会员信息** 中使用的 API。**获取会员基础信息 **中不含有 alipay.user.info.share。<br />**注意：**小程序“获取会员信息”已于2019 年5月25日升级为 **获取会员基础信息**，在此日期之前未签约 **获取会员信息 **的小程序应用无法再调用 alipay.user.info.share。 

### 小程序实现登录功能

1. 进入 [开放平台控制台](https://open.alipay.com/develop/manage) 的 对应小程序详情页 > **产品绑定** 绑定 **获取会员基础信息**。![](https://cdn.nlark.com/yuque/0/2022/png/179989/1661932867345-356a598e-9622-4c6d-b796-cea01549d7d2.png#align=left&display=inline&height=576&margin=%5Bobject%20Object%5D&originHeight=576&originWidth=1872&status=done&style=none&width=1872)
2. 绑定** 获取会员基础信息** 后：
   - 获取用户支付宝 user_id 请参考用户授权 my.getAuthCode 与 [alipay.system.oauth.token](https://opendocs.alipay.com/open/02xtla) 接口获取 user_id 参数。
   - 获取用户的昵称、头像、省份等信息需要调用前端组件 [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) 方法。

 
