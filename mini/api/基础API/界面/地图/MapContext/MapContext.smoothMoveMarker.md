# 简介

**MapContext.smoothMoveMarker** 用于标记点（marker）在地图上进行滑动动画。只有在**动画过程中** `action:'stop'` 才可以生效。

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
  markerId: 0, // 确保此时 marker 已在地图上
  targetDistances: [100, 200, 300, 600],
  points: aniPoints,
});

// 若希望 2 秒后停止 markerId 为 0 的动画，并将点标记移至终点。代码如下：
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
| markerId | Number | 是 | 执行动画的 marker 的 id，确保此时 marker 已经在地图上。 |
| markerData | Object | 否 | 传入 marker 对象。 只有 markerId 指向 markerData 中的 id 时才会生效  |
| points | Array | 是 | 动画路线的经纬度集合。 建议路线集合中第一个点的经纬度等于需要执行动画的 marker 点经纬度，这样可以使动画看起来更顺滑 |
| duration | Number | 否 | 动画执行时间，默认为 5000 毫秒（ms）。 |
| targetDistances | Array | 否 | 指定需要 onMarkerMove 回调的目标距离数组。 |
| action | String | 否 | 指定操作动画。<ul><li>`action:'stop'` 表示在动画过程中提前停止动画，并将点标记移动至动画路线最终位置。</li><li>`action:'start'` 默认值，表示执行动画。</li></ul> |

## 回调事件

| **回调事件** | **类型** | **描述** |
| --- | --- | --- |
| onMarkerMove | Function | 在指定距离点的回调事件。<br />具体对象值请参见下方 onMarkerMove 对象表。 |
| onMarkerMoveEnd | Function | 动画结束的回调事件。 |

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
