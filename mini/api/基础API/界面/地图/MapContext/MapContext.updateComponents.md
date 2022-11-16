# 简介

**MapContext.updateComponents** 是更新[地图属性](https://opendocs.alipay.com/mini/component/map#)的接口。地图属性包含中心经纬度，缩放级别，点标记，点标记动画，多段线，视野范围延伸，设置等。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.updateComponents({
  scale: 14,//缩放级别
  longitude: 120.131441,//中心经度
  latitude: 30.279383,//中心维度
  command: {
    // marker动画
    markerAnim: [
      {
        type: 0, // 跳动动画 10.1.35
        markerId: 'markerId',
      },
    ],
  },
  setting: {
    // 手势
    gestureEnable: true, // false 或 true
    // 比例尺
    showScale: true, // false 或 true
    // 指南针
    showCompass: true, // false 或 true
    // 双手下滑
    tiltGesturesEnabled: true, // false 或 true
    // 交通路况展示
    trafficEnabled: true, // false 或 true
    // 地图POI信息
    showMapText: true, // false 或 true
    // 高德地图logo位置
    logoPosition: { centerX: 150, centerY: 90 },
  },
  markers: [{}, {}],
  polyline: [{}, {}],
  'include-points': [{}, {}],
  'include-padding': { left: 0, right: 0, top: 0, bottom: 0 },
});
```

## 入参

| **属性**        | **类型** | **描述**                                 |
| --------------- | -------- | ---------------------------------------- |
| latitude        | Number   | 中心纬度。                               |
| longitude       | Number   | 中心经度。                               |
| scale           | Number   | 缩放级别，取值范围为 5-18。默认值为 16。 |
| markers         | Array    | 覆盖物，在地图上的一个点绘制图标。格式详见 [markers](https://opendocs.alipay.com/mini/component/map#markers)  。      |
| polyline        | Array    | 覆盖物，多个连贯点的集合（路线）。格式详见 [polyline](https://opendocs.alipay.com/mini/component/map#polyline)。可清除或选择性保留由 smoothMovePolyline 绘制的轨迹 |
| include-points  | Array    | 视野将进行小范围延伸包含传入的坐标。     |
| include-padding | Object   | 视野在地图 padding 范围内展示。          |
| setting         | Object   | 设置。                                   |
| command         | Object   | 命令，可用于更新 marker 动画。           |
