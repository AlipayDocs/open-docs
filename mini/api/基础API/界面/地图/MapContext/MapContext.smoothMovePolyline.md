# 简介

**MapContext.smoothMovePolyline** 是在地图上绘制轨迹动画的接口。只有在**动画过程中** `action:'stop'` 才可以生效，否则不会执行动画且不会绘制轨迹。。

## 使用限制
- iOS 上暂不支持 colorList 功能， iconPath 引用图片宽高需要为 2 的整数次幂。
- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 效果示例

  <image mode="scaleToFill" src="https://gw.alicdn.com/imgextra/i2/O1CN01LHEzcu20VdowedOub_!!6000000006855-1-tps-888-990.gif" style="width:300px; height: 350px;" />
  

# 接口调用

## 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
const aniPoints = [
  {
    latitude: 30.27296006944446,
    longitude: 120.12587239583334,
  }, {
    latitude: 30.27296006944446,
    longitude: 120.12457239583334,
  },
  {
    latitude: 30.27426006944446,
    longitude: 120.12457239583334,
  },
  {
    latitude: 30.27426006944446,
    longitude: 120.12657239583334,
  },
  {
    latitude: 30.27626006944446,
    longitude: 120.12657239583334,
  },
  {
    latitude: 30.27626006944446,
    longitude: 120.12727239583334,
  },
  {
    latitude: 30.27656006944446,
    longitude: 120.12727239583334,
  },
  {
    latitude: 30.27686006944446,
    longitude: 120.12987239583334,
  },
];
this.mapCtx.smoothMovePolyline({
  polylineId: 0,
  points: aniPoints,
  color: '#00FF00',
  width: 10,
  dottedLine: false,
  iconPath: '/image/map_alr.png',
  duration: 4000,// 动画时间设置为 4 秒
  iconWidth: 10,
});

// 若希望 2 秒后停止 polylineId 为 0 的轨迹动画，并将轨迹绘制完整。代码如下：
setTimeout(() => {
      this.mapCtx.smoothMovePolyline({
        polylineId: 0,
        action: 'stop',
      });
}, 2000);

```

## 入参

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| polylineId | Number | 是 | 执行动画的路线 ID。 |
| points | Array | 是 | 动画路线的经纬度集合。 |
| duration | Number | 否 | 动画执行时间，默认为 5000 毫秒（ms）。 |
| color | String | 否 | 轨迹动画的颜色。默认透明色。 |
| width | Number | 否 | 路线宽度。 |
| dottedLine | Boolean | 否 | 是否虚线。 |
| iconPath | String | 否 | 线的纹理地址。 |
| iconWidth | Number | 否 | 线的纹理宽度。设置 iconPath 后生效 |
| zIndex | Number | 否 | 动画的层级，zIndex 数值高的动画覆盖在低的上面 |
| colorList | Array | 否 | 彩虹线。如：`colorList:['#ff0000']` |
| action | String | 否 | 指定操作动画。<ul><li>`action:'stop'` 表示在动画过程中提前停止动画，并将轨迹绘制完整。</li><li>`action:'start'` 默认值，表示执行动画。</li></ul> |

## 回调事件

| **回调事件**      | **类型** | **描述**             |
| ----------------- | -------- | -------------------- |
| onPolylineMoveEnd | Function | 动画结束的回调事件。 |


# 常见问题 FAQ

## Q：在地图上使用 smoothMovePolyline 绘制的动画为什么无法使用 clearRoute 清除？

A：clearRoute 只能用于清除地图上的导航路线，无法清除 polyline 线路。请使用 MapContext.updateComponents 清除轨迹动画 示例如下：
```javascript
 this.mapCtx = my.createMapContext('map');

 //清除所有动画，代码如下：
 this.mapCtx.updateComponents({ polyline:[] }) 

 // map 上只保留 aniPoints 定义的线路轨迹，代码如下：
 this.mapCtx.updateComponents({
    polyline: [{
      points: aniPoints,
      color: '#0000FF',
      width: 10,
    }],
 })

```
