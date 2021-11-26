
# 简介
**MapContext.mapToScreen** 用于将地图经纬度坐标系转换成屏幕坐标系。

## 使用限制

- 基础库 [1.24.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.92 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
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
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| latitude | Number | 是 | 纬度。 |
| longitude | Number | 是 | 经度。 |


## 出参
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| x | Number | 横坐标。 |
| y | Number | 纵坐标。 |

