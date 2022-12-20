# 错误描述
小程序 [搜索关键词](https://opendocs.alipay.com/mini/02qjlz?ref=api) 提示 BIZ_ERROR（没有操作权限）。
```json
{"xxx_response":{"code":"40004","msg":"Business Failed","sub_code":"BIZ_ERROR","sub_msg":"没有操作权限"},"sign":"***"}
```

# 涉及接口
[alipay.open.search.orderdetail.query](https://opendocs.alipay.com/mini/02qlzz?ref=api)（查询搜索服务工单的详细信息）

# 错误原因
搜索服务工单的 appId，其所属的商家并未授权给当前操作用户。

# 解决方案

1. 确认接口alipay.open.search.orderdetail.query 入参中，apply_id 填写正确。
2. 确认当前账号具有操作该搜索服务工单中对应 app_id 的权限，如无，则需要该 app_id 所属的商家授权给当前操作的商家。
