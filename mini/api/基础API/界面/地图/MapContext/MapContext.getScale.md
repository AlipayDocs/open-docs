
# 简介
**MapContext.getScale** 用于获取地图的缩放级别。

## 使用限制

- 基础库 [1.24.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.92 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.getScale({
  success: res => {
    console.log(res.scale);
  }
});
```

## 出参
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| scale | Number | 缩放级别。取值范围为 5-18。默认值为 16。 |

