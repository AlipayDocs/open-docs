# 简介

**my.createMapContext** 是创建并返回一个地图上下文对象 [mapContext](https://opendocs.alipay.com/mini/api/mapcontext) 的 API。<br />相关 map 组件的属性，可查看 [map 地图](https://opendocs.alipay.com/mini/component/map)。

## 使用限制

- 需在 onReady 回调中（ map 组件初始化完成后 ）执行 my.createMapContext。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/map?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .axml 示例代码
```javascript
// .axml 
<map id='map'></map>
```
### .js 示例代码

```javascript
// .js
Page({
  onReady() {
    // 使用 my.createMapContext 获取 map 上下文
    this.mapCtx = my.createMapContext('map');
  },
});
```

#### PageContext.setData(Object)

初始化或重置地图数据，参数可选。

**基础库** [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本开始支持；**支付宝客户端** 10.1.32 或更高版本开始支持，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
```javascript
// .js
this.setData({
  // 缩放级别
  scale: 14,
  // 中心经度
  longitude: 120.131441,
  // 中心纬度
  latitude: 30.279383,
  // 是否显示带有方向的当前定位点
  'show-location': true,
  // 地图贴图 10.1.35 新增
  'ground-overlays': [
    {
      'include-points': [
        {
          // 右上
          latitude: 39.935029,
          longitude: 116.384377,
        },
        {
          // 左下
          latitude: 39.939577,
          longitude: 116.388331,
        },
      ],
      image: '/image/groundoverlay.png',
      alpha: 0.75,
      zIndex: 0,
    },
  ],
  // 网格贴图 10.1.35 新增
  'tile-overlay': {
    url: 'http://xixi.fullspeed.cn/public/map',
    type: 0,
    tileWidth: 256,
    tileHeight: 256,
    zIndex: 1,
  },
  // 点标记数组
  markers: [{
    latitude: 39.935029,
    longitude: 116.384377,
  }, {
    latitude: 39.939577,
    longitude: 116.388331,
  }],
  // 10.1.35 新增全览逻辑,视野在地图 padding 范围内展示
  'include-padding': { left: 10, right: 10, top: 10, bottom: 10 },
  // 多段线
  polyline: [{
    latitude: 39.935029,
    longitude: 116.384377,
  }, {
    latitude: 39.939577,
    longitude: 116.388331,
  }],
  // 初始化支持地图设置 10.1.50 新增
  setting: {
    // 手势,打开 1,关闭 0
    gestureEnable: 0,
    // 比例尺,显示 1,隐藏 0
    showScale: 0, 
    // 指南针,显示 1,隐藏 0
    showCompass: 0,
    // 双手下滑,打开 1,关闭 0
    tiltGesturesEnabled: 0,
    // 交通路况展示,显示 1,隐藏 0
    trafficEnabled: 0,
    // 地图 POI 信息,显示 1,隐藏 0
    showMapText: 0,
    // 高德地图 logo 位置
    logoPosition: { centerX: 150, centerY: 90 },
  },
});
```

## 入参

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| mapId | String | 是 | [map 地图](https://opendocs.alipay.com/mini/component/map) 的 ID。 |

## 返回值

返回值为 [MapContext](https://opendocs.alipay.com/mini/api/mapcontext)。

## 错误码

错误码信息可查看：

- [Andriod 地图错误码对照表](https://lbs.amap.com/api/android-sdk/guide/map-tools/error-code)
- [iOS 地图错误码对照](https://lbs.amap.com/api/ios-sdk/guide/map-tool/errorcode/)
