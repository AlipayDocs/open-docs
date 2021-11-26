
# 简介
**MapContext.showsCompass** 用于设置指南针是否可见。

- 1：可见 。
- 0：不可见。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.showsCompass({isShowsCompass:1});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| isShowsCompass | Int | 是 | 指南针是否可用。 |

