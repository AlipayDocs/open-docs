# 简介
**MapContext.setCenterOffset** 用于设置地图中心点偏移。向后向下为增长，屏幕比例范围为 (0~1)，默认偏移为 [0.5, 0.5]。

## 使用限制

- 基础库 [2.6.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.2.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.setCenterOffset({
  offset:[0.3,0.6]
});
```

## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| offset | `Array<Number>` | 是 | 偏移量。为两位数组。 |
