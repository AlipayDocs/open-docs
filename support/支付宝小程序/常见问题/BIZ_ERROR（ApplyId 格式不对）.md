# 错误描述
小程序 [搜索关键词](https://opendocs.alipay.com/mini/02qjlz?ref=api) 提示 BIZ_ERROR（ApplyId 格式不对）。
```json
{"xxx_response":{"code":"40004","msg":"Business Failed","sub_code":"BIZ_ERROR","sub_msg":"ApplyId 格式不对"},"sign":"***"}
```

# 涉及接口
[alipay.open.search.orderdetail.query](https://opendocs.alipay.com/mini/02qlzz?ref=api)（查询搜索服务工单的详细信息）

# 错误原因
接口请求参数中，applyId 的格式不规范。

# 解决方案

1. 确认接口 alipay.open.search.orderdetail.query 入参中，apply_id 已填写。
2. 确认接口 alipay.open.search.orderdetail.query 入参中，apply_id 是以 AP 开头的字符串。
