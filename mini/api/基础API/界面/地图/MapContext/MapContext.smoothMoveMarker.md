# 简介

**MapContext.smoothMoveMarker** 沿指定路径平滑移动 marker。

也可使用此 API 结束进行中的 marker 动画（入参 action 字段传 'stop'）。

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

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
  <view onTap="smoothMoveMarker">滑动 marker</view>
</view>
```

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
      // 需执行动画的 marker id
      markerId: 10, 
      // 需要执行动画的 marker 对象
      markerData: {
        id: 10,
        latitude: 30.261775,
        longitude: 120.102507 ,
        width: 19,
        height: 31,
        iconPath: 'https://gw.alipayobjects.com/mdn/rms_dfc0fe/afts/img/A*x9yERpemTRsAAAAAAAAAAAAAARQnAQ',
      },
      // 经纬度数组，指定移动路径
      points: aniPoints,
      // 经过距起点 100m、200m、300m、600m 的位置时，触发 onMarkerMove 事件
      targetDistances: [100, 200, 300, 600],
      success: res => {
        console.log('success' + JSON.stringify(res))
      },
      fail: err =>{
        console.log('err' + JSON.stringify(err))
      },
      complete: res => {
        console.log('complete' + JSON.stringify(res))
      }
    });
    
    setTimeout(() => {
      this.mapCtx.smoothMoveMarker({
        markerId: 10,
        action: 'stop', // 停止动画（marker 会被直接移到终点）
      });
    }, 2000);
  },
  
  markermove(e) {
    my.alert({ content: 'markerMove: ' + JSON.stringify(e.detail) });
  },
  
  markermoveend(e) {
    my.alert({ content: 'markermoveEnd: ' + JSON.stringify(e.detail) });
  },
});
```

## 入参

| **属性** | **类型** | **必填** | **描述** |
| --- | ------------- | --------- | --- |
| markerId | Number | 是 | 执行滑动的 marker 的 id |
| markerData | Object | 否 | 执行滑动的 marker 数据。传入时，将使用此数据新建一个 marker 进行滑动。marker 对象中的 id 必须等于 markerId。<br />详见 **Object markerData**。  |
| points | Array\<Object\> | 是 | 经纬度数组，确定移动路径。数组每个元素应包含 latitude 和 longitude 属性。<br />建议起点经纬度与滑动的 marker 本身经纬度相同。 |
| duration | Number | 否 | 移动时间，默认值为 5000，单位毫秒。 |
| targetDistances | Array | 否 | 指定需要 onMarkerMove 回调的目标距离数组。详见后文 **事件回调**。 |
| action | String | 否 | 操作类型。'start'（默认值）表示开始移动。'stop' 表示结束移动，marker 直接移到终点。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 |调用结束的回调函数（调用成功、失败都会执行）。 |

### Object markerData 

| **属性** | **类型** | **必填** | **描述** |
| --------- | --------| --------  | ----------------------------------- |
| id          | Number   | 是   | 标记点 ID。 |
| latitude       | Number   | 是    | 纬度。                              |
| longitude      | Number   | 是    | 经度。                              |
| iconPath | String     | 是   | 图标的图片路径，为小程序包文件路径，如：/pages/image/test.jpg。不支持相对路径。 |
| width      | Number   | 否   | 图标的宽度。   |
| height      | Number   | 否   | 图标的高度。    |

## 事件回调
marker 移动过程中会触发 MarkerMove 和 MarkerMovEnd 事件。需通过 map 组件注册其回调函数，如：`<map id="map" onMarkerMove="markermove" onMarkerMoveEnd="markermoveend"></map>`

### onMarkerMove
marker 移动经过 targetDistances 中的每个距离时，触发此事件。回调函数将收到一个 Object 类型的参数，包含如下属性：
| **属性**       | **类型** | **描述**                            |
| -------------- | -------- | ----------------------------------- |
| longitude      | Number   | 经度。                          |
| latitude       | Number   | 纬度。                          |
| targetDistance | Number   | 距起点的距离。                   |
| index          | Number   | 当前 targetDistance 在 targetDistances 中的索引。 |

### onMarkerEnd
marker 移动结束时，触发此事件

## 错误码

fail 回调函数的参数为 Object 类型，其 error 属性为错误码，errorMessage 为错误消息。

| **错误码**       | **说明** | **解决方案**                            |
| -------------- | -------- | ----------------------------------- |
| 2          | 参数错误   | points 数组长度须大于 1。 |
| 10001      | 未指定 marker   | 传入有效的 markerId。 |
