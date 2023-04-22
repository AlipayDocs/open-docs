# 简介

**my.createMapContext** 创建用于 [MapContext](https://opendocs.alipay.com/mini/api/mapcontext) 对象，用于操作地图组件。

请在 Page.onReady 后调用。

## 使用限制

- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/map?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .axml 示例代码
```html
<map id='map'></map>
```
### .js 示例代码
```javascript
Page({
  onReady() {
    this.mapCtx = my.createMapContext('map');
  },
});
```

## 入参

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| mapId | String | 是 | [map 地图](https://opendocs.alipay.com/mini/component/map) 的 ID。 |

## 返回值

返回值为 [MapContext](https://opendocs.alipay.com/mini/api/mapcontext)。
