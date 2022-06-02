# 简介
**MapContext.setMapType** 用于设置地图主题类型。

## 使用限制

- 基础库 [1.24.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.92 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.setMapType({
  mapType:1
});
```

## 入参
| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| mapType | Int | 是 | 地图主题类型。支持类型如下：<ul><li>0：标准地图；</li><li>1：卫星地图。</li></ul> |
