
# 简介
判断矩形区域是否包含传入的经纬度点。

## 使用限制

- 基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端版本 10.2.33 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器暂不支持模拟，请以真机调试效果为准。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
this.mapCtx = my.createMapContext('map');
this.mapCtx.polygonContainsPoint({
  polygon: [
    { // 左上
      latitude: 30.278467,
      longitude: 120.048859
    },
    { // 右上
      latitude: 30.280691,
      longitude: 120.086796
    },
    { // 右下
      latitude: 30.2629,
      longitude: 120.091088
    },
    { // 左下
      latitude: 30.247331,
      longitude: 120.044911
    }
  ],
  point: {
    longitude: 120.061219,
    latitude: 30.26972
  },
  success(e) {
    my.alert({
      content: "include result:" + e.success
    });
  },
  fail(e) {
    my.alert({
      content: "failed:" + e.errorMessge + " error:" + e.error
    });
  }
});
```

## 入参
| **属性** | **类型** | **默认值** | **必填** | **说明** |
| --- | --- | --- | --- | --- |
| polygon | Array |  | 是 | 矩形区域的经纬度范围。 |
| point | Object |  | 是 | 经纬度度的值。 |


### polygon 的元素和 point 对象
| **属性** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |
| latitude | Number | 是 | 纬度 |
| longitude | Number | 是 | 经度 |


### success 返回值
| **属性名** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | <ul><li>true：在矩形区域内。</li><li>false：不在矩形区域内。</li></ul> |

