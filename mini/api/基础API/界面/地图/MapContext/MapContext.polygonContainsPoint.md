# 简介

**MapContext.polygonContainsPoint** 是根据指定的经纬度数据确定多边形区域，判断区域内是否包含指定经纬度的 API。

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
  // 左上
  {
    latitude: 30.273960,
    longitude: 120.124872,
  },
  // 左下
  {
    latitude: 30.271960,
    longitude: 120.124872,
  },
  // 右下
  {
    latitude: 30.271960,
    longitude: 120.126872,
  },
  // 右上
  {
    latitude: 30.273960,
    longitude: 120.126872,
  },
];
this.mapCtx.polygonContainsPoint({
  // 经纬度数组，确定多边形区域
  polygon: points,
  // 需要判断位置的经纬度点
  point: {
    latitude: 30.272960,
    longitude: 120.126872,
  },
  success(e) {
    my.alert({
      content: 'success--->' + JSON.stringify(e),
    });
  },
  fail(e) {
    my.alert({
      content: 'fail--->' + JSON.stringify(e),
    });
  },
  complete(e) {
    my.alert({
      content: 'complete--->' + JSON.stringify(e),
    });
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型**        | **必填** | **描述**               |
| -------- | --------------- | -------- | ---------------------- |
| polygon  | Array\<Object\> | 是       | 经纬度数组，确定多边形区域。 |
| point    | Object          | 是       | 需要判断位置的经纬度点。  |
| success  | Function        | 否       | 调用成功的回调函数。   |
| fail  | Function        | 否       | 调用失败的回调函数。   |
| comp  | Function        | 否       | 调用成功的回调函数。   |

### Object polygon/point

| **参数**  | **类型** | **必填** | **描述** |
| --------- | -------- | -------- | -------- |
| latitude  | Number   | 是       | 纬度。   |
| longitude | Number   | 是       | 经度。   |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | <ul><li>true：在多边形区域内。</li><li>false：不在多边形区域内。</li></ul> |


## 错误码

| **错误码**       | **说明** | **解决方案**                            |
| -------------- | -------- | ----------------------------------- |
| 2          | 限 iOS 环境。参数错误   | 请检查参数 polygon 和 point 格式是否正确 |
| 60103          | 限安卓环境。参数错误   | 请检查参数 polygon 和 point 格式是否正确 |
