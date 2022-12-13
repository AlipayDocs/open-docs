# 简介

**MapContext.smoothMoveMarker** 沿指定路线滑动 marker。 `action:'stop'` 可停止滑动，在**滑动过程中**使用时可停止滑动并将标记点放至指定路线终点。

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
const aniPoints = [
  {
    latitude: 30.261775,
    longitude: 120.102507,
  },
  {
    latitude: 30.262794,
    longitude: 120.103816,
  },
  {
    latitude: 30.264036,
    longitude: 120.10491,
  },
  {
    latitude: 30.265194,
    longitude: 120.10609,
  },
  {
    latitude: 30.265824,
    longitude: 120.107217,
  },
  {
    latitude: 30.267446,
    longitude: 120.109749,
  },
  {
    latitude: 30.268715,
    longitude: 120.112721,
  },
];
this.mapCtx.smoothMoveMarker({
  // 需要执行动画的 marker 的 id
  markerId: 0, 
  // 传入一个需要执行动画的 marker 对象
  markerData: {
    id: 0,
    latitude: 30.261775,
    longitude: 120.102507 ,
    width: 19,
    height: 31,
    iconPath: 'https://gw.alipayobjects.com/mdn/rms_dfc0fe/afts/img/A*x9yERpemTRsAAAAAAAAAAAAAARQnAQ',
  },
  targetDistances: [100, 200, 300, 600],
  points: aniPoints,
});

// 2 秒后停止 markerId 为 0 的 marker 的滑动，并将点标记放至 points 路线终点。代码如下：
setTimeout(() => {
      this.mapCtx.smoothMoveMarker({
        markerId: 0,
        action: 'stop',
      });
}, 2000);
```

## 入参

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| markerId | Number | 是 | 执行滑动的 marker 的 id |
| markerData | Object | 否 | marker 对象。 当 markerId 等于 markerData 中的 id 时，这个 marker 对象就会在地图上显示出来并沿指定路线滑动。  |
| points | Array | 是 | 滑动路线的经纬度集合。 建议路线集合中第一个点的经纬度等于需要执行滑动的 marker 点经纬度，这样可使滑动效果更顺滑 |
| duration | Number | 否 | 滑动执行时间，默认为 5000 毫秒（ms）。 |
| targetDistances | Array | 否 | 指定需要 onMarkerMove 回调的目标距离数组。 |
| action | String | 否 | 指定操作滑动。<ul><li>`action:'stop'` 表示在滑动过程中提前停止滑动，并将点标记移动至指定线路终点位置。</li><li>`action:'start'` 默认值，表示执行滑动。</li></ul> |

## 回调事件

| **回调事件** | **类型** | **描述** |
| --- | --- | --- |
| onMarkerMove | Function | 在指定距离点的回调事件。<br />具体对象值请参见下方 onMarkerMove 对象表。 |
| onMarkerMoveEnd | Function | 滑动结束的回调事件。 |

### onMarkerMove 对象

| **属性**       | **类型** | **描述**                            |
| -------------- | -------- | ----------------------------------- |
| index          | Number   | 目标点在 targetDistances 中的索引。 |
| targetDistance | Array    | 目标点的距离。                      |
| latitude       | Number   | 纬度。                              |
| longitude      | Number   | 经度。                              |

### 回调事件示例代码

```html
<view>
  <map
    id="map"
    longitude="120.131441"
    latitude="30.279383"
    scale="{{scale}}"
    controls="{{controls}}"
    onControlTap="controltap"
    markers="{{markers}}"
    onMarkerTap="markertap"
    polyline="{{polyline}}"
    circles="{{circles}}"
    onRegionChange="regionchange"
    onTap="tap"
    onCalloutTap="callouttap"
    onMarkerMove="markermove"
    onMarkerMoveEnd="markermoveend"
    show-location
    style="width: 100%; height: 200px;"
    include-points="{{includePoints}}"
    ground-overlays="{{ground-overlays}}"
  >
  </map>
</view>
```

```javascript
// .js

Page({
  markermove(e) {
    my.alert({ content: 'markerMove: ' + JSON.stringify(e.detail) });
  },
  markermoveend(e) {
    my.alert({ content: 'markermoveEnd: ' + JSON.stringify(e.detail) });
  },
});
```
