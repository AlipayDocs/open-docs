# 简介

**MapContext.clearRoute** 用于清除地图上的[导航路线](https://opendocs.alipay.com/mini/api/uwffxx)。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
this.mapCtx = my.createMapContext('map');
this.mapCtx.clearRoute();
```
