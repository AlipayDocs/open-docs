# 简介

**MapContext.mapToScreen** 用于将地图经纬度坐标系转换成屏幕坐标系。

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
this.mapCtx.mapToScreen({
  latitude:30.202041,
  longitude:120.108257,
  success: res => {
    console.log(res);
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| latitude | Number | 是 | 纬度。 |
| longitude | Number | 是 | 经度。 |
| success | Function | 否 | 调用成功的回调函数。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| x | Number | 横坐标。 |
| y | Number | 纵坐标。 |
