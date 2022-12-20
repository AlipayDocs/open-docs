# 错误描述
小程序 [搜索关键词](https://opendocs.alipay.com/mini/02qjlz?ref=api) 提示 BIZ_ERROR（请求入参翻译失败）。
```json
{"xxx_response":{"code":"40004","msg":"Business Failed","sub_code":"BIZ_ERROR","sub_msg":"请求入参翻译失败"},"sign":"***"}
```

# 涉及接口
[alipay.open.search.baseorder.modify](https://opendocs.alipay.com/mini/02qm00?ref=api)（搜索运营提报基础信息工单）

# 错误原因
接口请求参数中，base_items 的格式、字段不规范。

# 解决方案
确认接口 alipay.open.search.baseorder.modify 入参中，base_items 参数存在且能正常被解析。
