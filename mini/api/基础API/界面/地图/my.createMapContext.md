
# 简介
**my.createMapContext** 是创建并返回一个地图上下文对象 [mapContext](api/mapcontext) 的 API。<br />相关组件详情，请参见 [**地图**](/mini/component/map)[map](/mini/component/map)。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-map?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
//.axml 
<view class="page-section">
      <map
        id="map"
        customMapStyle="light"
        longitude="{{longitude}}"
        latitude="{{latitude}}"
        scale="{{scale}}"
        controls="{{controls}}"
        onControlTap="controltap"
        markers="{{markers}}"
        onMarkerTap="markertap"
        polyline="{{polyline}}"
        polygon="{{polygon}}"
        circles="{{circles}}"
        onRegionChange="regionchange"
        onTap="tap"
        onCalloutTap="callouttap"
        show-location style="width: 100%; height: 200px;"
        include-points="{{includePoints}}"
        ground-overlays="{{ground-overlays}}">
      </map>
  </view>
```

### .js 示例代码
```javascript
//.js
Page({
  // ... ...
  onReady() {
    // 使用 my.createMapContext 获取 map 上下文
    this.mapCtx = my.createMapContext('map');
  },
  // ... ...
}）
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| mapId | String | 是 | [﻿map 组件](https://opendocs.alipay.com/mini/component/map) 的 ID。 |


## 返回值
返回值为 [MapContext](api/mapcontext)。

## PageContext.setData(Object)
初始化或重置地图数据，参数可选。<br />**基础库** [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本开始支持；**支付宝客户端** 10.1.32 或更高版本开始支持，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。

### 示例代码
```javascript
//  .js
this.setData({
    scale: 14,
    longitude: 120.131441,
    latitude: 30.279383,
    'show-location':true,
    // 地图贴图 10.1.35 新增
    'ground-overlays':[{
        'include-points':[{// 右上
            latitude: 39.935029,
            longitude: 116.384377,
          },{// 左下
            latitude: 39.939577,
            longitude: 116.388331,
          }],
        image:'/image/groundoverlay.png',
        alpha:0.75,
        zIndex:0,
    }],
    // 网格贴图 10.1.35 新增
    'tile-overlay':{
      url:'http://xixi.fullspeed.cn/public/map',
      type:0,
      tileWidth:256,
      tileHeight:256,
      zIndex:1,
    },
    markers:[{},{}],
    'include-points':[{},{}],
    // 10.1.35 新增全览逻辑
    'include-padding':{left:0, right:0, top:0, bottom:0},
    polyline: [{},{}],
    circles: [{},{}],
    controls: [{},{}],
    polygon: [{},{}],
    'include-padding':{},
    // 初始化支持地图设置 10.1.50 新增
    setting:{
        // 手势
        gestureEnable:0/1,
        // 比例尺
        showScale:0/1,
        // 指南针
        showCompass:0/1,
        // 双手下滑
        tiltGesturesEnabled:0/1,
        // 交通路况展示
        trafficEnabled:0/1,                     
        // 地图POI信息
        showMapText:0/1, 
        // 高德地图logo位置
        logoPosition:{centerX:150, centerY:90},                       
    },
});
```

## 错误码
错误码信息请参见：

- [Andriod 地图错误码对照表](https://lbs.amap.com/api/android-sdk/guide/map-tools/error-code)
- [iOS 地图错误码对照](https://lbs.amap.com/api/ios-sdk/guide/map-tool/errorcode/)
