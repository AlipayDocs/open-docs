# 简介
**MapContext.smoothMovePolyline** 是轨迹动画。

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js
this.mapCtx = my.createMapContext('map');
const aniPoints = [{
      latitude: 30.261775,
      longitude: 120.102507,
    },{
      latitude: 30.262794,
      longitude: 120.103816,
    },{
      latitude: 30.264036,
      longitude: 120.10491,
    },{
      latitude: 30.265194,
      longitude: 120.10609,
    },{
      latitude: 30.265824,
      longitude: 120.107217,
    },{
      latitude: 30.267446,
      longitude: 120.109749,
    },{
      latitude: 30.268715,
      longitude: 120.112721,
    }
];
this.mapCtx.smoothMovePolyline({
      polylineId: 0,
      points: aniPoints,
      color: '#FF0000DD',
      width: 10,
      dottedLine: false,
      iconPath: "/image/map_alr.png",
      iconWidth:10,
})
```

## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| polylineId | Number | 是 | 执行动画的路线 ID。 |
| points | Array | 是 | 动画路线的经纬度集合。 |
| duration | Number | 否 | 动画执行时间，默认为 5000 毫秒（ms）。 |
| color | String | 否 | 轨迹动画的颜色。 |
| width | Number | 否 | 路线宽度。 |
| dottedLine | Boolean | 否 | 是否虚线。 |
| iconPath | String | 否 | 线的纹理地址。 |
| iconWidth | Number | 否 | 线的纹理宽度。 |
| zIndex | Number | 否 | 线的 Z 轴坐标。 |
| iconPath | String | 否 | 纹理的资源地址。 |
| colorList | Array | 否 | 彩虹线。 |
| action | String | 否 | 指定操作动画。<ul><li>`action:'stop'` 表示提前结束动画。</li></ul> |

## 回调事件
| **回调事件** | **类型** | **描述** |
| --- | --- | --- |
| onPolylineMoveEnd | Function | 动画结束的回调事件。 |
