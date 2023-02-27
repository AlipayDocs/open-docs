# 简介

**MapContext.moveToLocation** 移动地图中心位置。

可将地图中心移动到当前定位位置或任意经纬度。前者需要配合设置 map 组件的 show-location 属性（参见示例代码）。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码
```html
<view>
  <map id="map" show-location style="width: 100%; height: 200px;"></map>
</view>
```

### .js 示例代码
```javascript
this.mapCtx = my.createMapContext('map');

// 调用方式一：将地图中心移动到当前定位位置
this.mapCtx.moveToLocation();

// 调用方式二：将地图中心移动到指定经纬度
this.mapCtx.moveToLocation({ 
  latitude: 39.9,
  longitude: 116.39,
});
```

## 入参

| **属性**  | **类型** | **必填** | **描述** |
| --------- | -------- | -------- | -------- |
| longitude | Number   | 否       | 经度。支付宝客户端 10.2.8 开始支持。 |
| latitude  | Number   | 否       | 纬度。支付宝客户端 10.2.8 开始支持。 |

## 错误码

fail 回调函数将收到一个 Object 类型的参数，基本 error 属性为错误码，errorMessage 为错误消息

| **错误码** | **错误消息**       | **解决方案**                               |
| ---------- | -------------- | ------------------------------------------ |
| 6000       | 未允许定位 | 入参指定经纬度，或在 map 组件中添加 show-location。 |

## Bug & Tip

- MapContext.moveToLocation 的调用也会导致地图被设置为默认缩放级别（16）。

