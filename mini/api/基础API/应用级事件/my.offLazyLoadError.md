# 简介
移除小程序异步组件（[懒加载插件](https://opendocs.alipay.com/mini/plugin/plugin-usage#%E6%87%92%E5%8A%A0%E8%BD%BD%E6%A8%A1%E5%BC%8F)、[分包异步化](https://opendocs.alipay.com/mini/057ht3)）加载失败事件监听函数。

## 使用限制

- 基础库 [2.8.1](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
const listener = function (res) { console.log(res) }
my.onLazyLoadError(listener)
my.offLazyLoadError(listener) // 需传入与监听时同一个的函数对象
```

## 入参
| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| callback | Function | 否 | 传入 onLazyLoadError 传入的监听函数。不传此参数则移除所有监听函数。 |
