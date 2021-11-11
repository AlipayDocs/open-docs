
# 简介
在页面间通信中触发一个事件。

## 使用限制

- 版本要求基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 入参
入参结构为：(String eventName, Any[] ...args)。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| eventName | String | 是 | 需要触发的事件的名称。 |
| args | Any[] | 否 | 事件的参数。 |
