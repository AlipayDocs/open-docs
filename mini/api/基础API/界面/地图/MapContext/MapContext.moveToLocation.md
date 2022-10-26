# 简介

**MapContext.moveToLocation** 用于移动视野到指定坐标点并恢复到默认缩放级别，需要配合 [map 组件](/mini/component/map) 的 show-location 使用。

支付宝客户端 10.2.8 或更高版本支持将地图中心移动到指定位置。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 支持在插件内调用。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.moveToLocation({ latitude: 39.9, longitude: 116.39 });
```

## 入参

| **属性**  | **类型** | **必填** | **描述** |
| --------- | -------- | -------- | -------- |
| longitude | Number   | 否       | 经度。默认为当前定位点的经度   |
| latitude  | Number   | 否       | 纬度。默认为当前定位点的维度   |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### 返回值

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**     |
| -------- | -------- | ------------ |
| success     | Boolean   | 是否执行。 |

## 错误码

| **错误码** | **描述**       | **解决方案**                               |
| ---------- | -------------- | ------------------------------------------ |
| 3        | 没有设置入参且 map 组件没有使用 show-location | map 组件中添加上 show-location，目前仅支持安卓环境 |
