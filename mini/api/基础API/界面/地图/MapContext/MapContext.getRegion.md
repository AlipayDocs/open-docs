# 简介

**MapContext.getRegion** 可获取地图东北角、西南角的经纬度，从而获取地图整体的视野范围。

![|399x225](http://mdn.alipayobjects.com/afts/img/A*9KnRSZHPtBZ9xbJMl2ucnwBkAa8wAA/original?bz=openpt_doc&t=FDATT4LmNWYCQJlzrCcm0QAAAABkMK8AAAAA#align=left&display=inline&height=225&margin=%5Bobject%20Object%5D&originHeight=225&originWidth=399&status=done&style=stroke&width=399)

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.getRegion({
  success: res => {
    console.log(res);
  },
});
```

## 返回示例

### success 回调返回示例

执行成功时，触发 success 回调，回调参数示例如下（已转换为 JSON 字符串）：

```json
// .json
{
  "northeast": {
    "latitude": 39.90159974373447,
    "longitude": 116.39376148581508
  },
  "southwest": {
    "latitude": 39.89839488008665,
    "longitude": 116.38624861836435
  }
}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述**             |
| -------- | -------- | -------- | -------------------- |
| success  | Function | 否       | 调用成功的回调函数。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**  | **类型** | **描述**             |
| --------- | -------- | -------------------- |
| southwest | Object   | 地图的西南角经纬度。 |
| northeast | Object   | 地图的东北角经纬度。 |
