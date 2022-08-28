# 简介

**MapContext.getCenterLocation** 用于获取当前地图中心位置。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.getCenterLocation({
  success: res => {
    my.alert({
      content: 'longitude:' + res.longitude + '\nlatitude:' + res.latitude,
    });
    console.log(res.longitude);
    console.log(res.latitude);
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

### success 返回值

Object 类型，属性如下：

| **属性**  | **类型** | **描述** |
| --------- | -------- | -------- |
| longitude | Number   | 经度。   |
| latitude  | Number   | 纬度。   |
