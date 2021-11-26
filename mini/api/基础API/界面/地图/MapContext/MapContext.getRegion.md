
# 简介
**MapContext.getRegion** 可获取地图东北角、西南角的经纬度，从而获取地图整体的视野范围。

![|399x225](http://mdn.alipayobjects.com/afts/img/A*9KnRSZHPtBZ9xbJMl2ucnwBkAa8wAA/original?bz=openpt_doc&t=FDATT4LmNWYCQJlzrCcm0QAAAABkMK8AAAAA#align=left&display=inline&height=225&margin=%5Bobject%20Object%5D&originHeight=225&originWidth=399&status=done&style=stroke&width=399)

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器暂不支持模拟，请以真机调试效果为准。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.getRegion({
  success: res => {
    console.log(res);
  }
});
```

### success 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| southwest | Object | 地图的西南角经纬度。 |
| northeast | Object | 地图的东北角经纬度。 |


## 返回值示例
```json
// .json
{
  "northeast":{"latitude":39.90159974373447,"longitude":116.39376148581508},
  "southwest":{"latitude":39.89839488008665,"longitude":116.38624861836435}
}
```
