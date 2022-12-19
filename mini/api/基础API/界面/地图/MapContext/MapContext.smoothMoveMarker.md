# 简介

**MapContext.smoothMoveMarker** 沿指定路线滑动点标记。 `action:'stop'` 可停止滑动，在**滑动过程中**使用时可停止滑动并将标记点放至指定路线终点。

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js
Page({
  smoothMoveMarker(){
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
      markerId: 1, 
      // 传入一个需要执行动画的 marker 对象
      markerData: {
        id: 1,
        latitude: 30.261775,
        longitude: 120.102507 ,
        width: 19,
        height: 31,
        iconPath: 'https://gw.alipayobjects.com/mdn/rms_dfc0fe/afts/img/A*x9yERpemTRsAAAAAAAAAAAAAARQnAQ',
      },
      // 距离起点 100m、200m、300m、600m 的经纬度坐标通过 onMarkerMove 回调事件返回
      targetDistances: [100, 200, 300, 600],
      // 经纬度数组，确定滑动线路
      points: aniPoints,
      // 参数正确则返回 true 
      success: res => {
        console.log('success' + JSON.stringify(res))
      },
      // 参数错误则返回错误码 
      fail: err =>{
        console.log('err' + JSON.stringify(err))
      },
      complete: res => {
        console.log('complete' + JSON.stringify(res))
      }
    });
    
    // 2 秒后停止 markerId 为 0 的 marker 的滑动，并将点标记放至 points 路线终点。    代码如下：
    setTimeout(() => {
          this.mapCtx.smoothMoveMarker({
            markerId: 0,
            action: 'stop',
          });
    }, 2000);
  },
  // targetDistances 指定距离点的回调事件
  markermove(e) {
    my.alert({ content: 'markerMove: ' + JSON.stringify(e.detail) });
  },
  // 滑动结束的回调事件
  markermoveend(e) {
    my.alert({ content: 'markermoveEnd: ' + JSON.stringify(e.detail) });
  },
});
```
```html
<!-- .axml-->
<view>
  <map
    id="map"
    longitude="120.131441"
    latitude="30.279383"
    onMarkerMove="markermove"
    onMarkerMoveEnd="markermoveend"
    style="width: 100%; height: 200px;"
  >
  </map>
  <view onTap="smoothMoveMarker">滑动点标记</view>
</view>
```
## 入参

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| markerId | Number | 是 | 执行滑动的 marker 的 id |
| markerData | Object | 否 | marker 对象。新建一个点标记进行滑动。marker 对象中的 id 必须等于 markerId。  |
| points | Array | 是 | 经纬度数组，确定滑动路线。 建议数组中第一个经纬度值等于需要执行滑动的 marker 点经纬度值，可使滑动效果更顺滑。 |
| duration | Number | 否 | 滑动执行时间，默认为 5000 毫秒（ms）。 |
| targetDistances | Array | 否 | 指定需要 onMarkerMove 回调的目标距离数组。**onMarkerMove** 详情见**回调事件**。 |
| action | String | 否 | 指定操作滑动。<ul><li>`action:'stop'` 表示在滑动过程中提前停止滑动，并将点标记移动至指定线路终点位置。</li><li>`action:'start'` 默认值，表示执行滑动。</li></ul> |
| success | Function | 否 | 参数正确的回调函数。 |
| fail | Function | 否 | 参数错误的回调函数。 |
| complete | Function | 否 |调用结束的回调函数（调用成功、失败都会执行）。 |

## 回调事件
回调事件需要在 map 中进行注册，js 中进行回调       
                          
例：`<map id="map" onMarkerMove="markermove" onMarkerMoveEnd="markermoveend"></map>`
| **回调事件** | **类型** | **描述** |
| --- | --- | --- |
| onMarkerMove | Function | 在指定距离点的回调事件。<br />详情见 **Function onMarkerMove**。 |
| onMarkerMoveEnd | Function | 滑动结束的回调事件。 |

### Function onMarkerMove 

| **属性**       | **类型** | **描述**                            |
| -------------- | -------- | ----------------------------------- |
| index          | Number   | 目标点在 targetDistances 中的索引。 |
| targetDistance | Array    | 目标点的距离。                      |
| latitude       | Number   | 纬度。                              |
| longitude      | Number   | 经度。                              |

## 错误码

| **错误码**       | **说明** | **解决方案**                            |
| -------------- | -------- | ----------------------------------- |
| 2          | 限安卓环境。参数错误   | points 数组长度需要大于等于 2 |
| 10001          | 未指定 marker   | 请给 markerId 赋值，值为需要执行动画的 marker 的 id。 |
