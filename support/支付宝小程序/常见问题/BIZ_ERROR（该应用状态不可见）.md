# 错误描述
小程序 [搜索关键词](https://opendocs.alipay.com/mini/02qjlz?ref=api) 提示BIZ_ERROR（该应用状态不可见）。
```json
{"xxx_response":{"code":"40004","msg":"Business Failed","sub_code":"BIZ_ERROR","sub_msg":"该应用状态不可见"},"sign":"***"}
```

# 涉及接口
[alipay.open.search.baseorder.modify](https://opendocs.alipay.com/mini/02qm00?ref=api)（搜索运营提报基础信息工单）

# 错误原因
该小程序的服务被隐藏，导致不可见。

# 解决方案

- alipay.open.search.baseorder.modify 检查传入的 APPID 是否正确。
- APPID 对应的小程序需要确保在服务库可见，登录 [商家平台](https://b.alipay.com/page/home) > **运营中心** > **小程序信息** > **基础信息**，开启小程序搜索可见。 ![](https://intranetproxy.alipay.com/skylark/lark/0/2022/png/21956847/1670221501460-e48e0410-593b-4970-bb39-891d68d2e60a.png#align=left&display=inline&height=306&margin=%5Bobject%20Object%5D&originHeight=1578&originWidth=2878&status=done&style=none&width=559)
