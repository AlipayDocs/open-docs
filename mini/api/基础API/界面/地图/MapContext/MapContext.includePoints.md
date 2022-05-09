# 简介

**MapContext.includePoints** 用于缩放视野到指定可视区域。

## 使用限制

- 基础库 [2.6.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.2.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.includePoints({
  points:[{
    latitude: 39.935029,
    longitude: 116.384377
  },{
    latitude: 39.939577,
    longitude: 116.388331,
  }],
  padding:[48,48,48,48]
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| points | Array\<Object\> | 是 | 要显示在可视区域内的坐标点列表。 |
| padding | Array\<Number\> | 否 | 坐标点形成的矩形边缘到地图边缘的距离。格式为 [上，右，下，左]，如果数据只有一项，则上下左右的 padding 一致。 |


### Object points
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| longitude | Number | 是 | 经度。 |
| latitude | Number | 是 | 纬度。 |

