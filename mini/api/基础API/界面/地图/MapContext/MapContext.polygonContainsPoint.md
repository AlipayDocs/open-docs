# 简介

**MapContext.polygonContainsPoint** 判断多边形区域是否包含指定的坐标点。

## 使用限制

- 基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端版本 10.2.33 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
var points = [
  {
    latitude: 30.273960,
    longitude: 120.124872,
  },
  {
    latitude: 30.271960,
    longitude: 120.124872,
  },
  {
    latitude: 30.271960,
    longitude: 120.126872,
  },
  {
    latitude: 30.273960,
    longitude: 120.126872,
  },
];
this.mapCtx.polygonContainsPoint({
  polygon: points,

  point: {
    latitude: 30.272960,
    longitude: 120.126872,
  },
  success(e) {
    my.alert({
      content: 'success--->' + JSON.stringify(e),
    });
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型**        | **必填** | **描述**               |
| -------- | --------------- | -------- | ---------------------- |
| polygon  | Array\<Object\> | 是       | 多边形区域的所有顶点坐标。 |
| point    | Object          | 是       | 需要判断位置的坐标点。  |
| success  | Function        | 否       | 调用成功的回调函数。   |
| fail  | Function        | 否       | 调用失败的回调函数。   |
| complete  | Function        | 否       | 调用结束的回调函数（调用成功、失败都会执行）。   |

### 坐标点

polygon 的数组元素和 point 参数为坐标点，包含以下属性：

| **属性**  | **类型** | **必填** | **描述** |
| --------- | -------- | -------- | -------- |
| latitude  | Number   | 是       | 纬度。   |
| longitude | Number   | 是       | 经度。   |

### Function success

success 回调函数会收到一个 Object 类型的参数，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | 指定的点是否在多边形区域内，true 在，false 不在。</li></ul> |


## 错误码

fail 回调函数会收到一个 Object 类型的参数，其 error 字段为错误码，errorMessage 为错误消息。

| **错误码**      | **错误消息** | **解决方案**                          |
| -------------- | -------- | ----------------------------------- |
| 2 或 60103      | 参数错误  | 请检查参数 polygon 和 point 格式是否正确。 |
