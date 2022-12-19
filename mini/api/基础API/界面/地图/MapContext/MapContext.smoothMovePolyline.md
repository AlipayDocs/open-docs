# 简介

**MapContext.smoothMovePolyline** 是按照指定的经纬度数据和时间，动态的在地图上绘制线的 API。`action:'stop'` 可停止绘制的动画，在**绘制的过程中**使用时可停止动画并将线路绘制完整。

## 使用限制
- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 效果示例

  <image mode="scaleToFill" src="https://gw.alicdn.com/imgextra/i2/O1CN01LHEzcu20VdowedOub_!!6000000006855-1-tps-888-990.gif" style="width:300px; height: 350px;" />
  

# 接口调用

## 示例代码
```html
<!-- .axml-->
<view>
  <map
    id="map"
    longitude="120.125872"
    latitude="30.272960"
    onPolylineMoveEnd="onPolylineMoveEnd"
    style="width: 100%; height: 200px;"
  >
  </map>
  <view onTap="smoothMovePolyline">制轨迹动画</view>
</view>
```

```javascript
// .js
Page({
  smoothMovePolyline(){
    this.mapCtx = my.createMapContext('map');
    const aniPoints = [
      {
        latitude: 30.272960,
        longitude: 120.125872,
      }, {
        latitude: 30.272960,
        longitude: 120.124572,
      },
      {
        latitude: 30.274260,
        longitude: 120.124572,
      },
      {
        latitude: 30.274260,
        longitude: 120.126572,
      },
      {
        latitude: 30.276260,
        longitude: 120.126572,
      },
      {
        latitude: 30.276260,
        longitude: 120.127272,
      },
      {
        latitude: 30.276560,
        longitude: 120.127272,
      },
      {
        latitude: 30.276860,
        longitude: 120.129872,
      },
    ];
    this.mapCtx.smoothMovePolyline({
      // 线 id
      polylineId: 10,
      // 经纬度数组，确定画线轨迹
      points: aniPoints,
      // 线路颜色
      color: '#00FF00',
      // 线路宽度
      width: 10,
      // 是否虚线
      dottedLine: false,
      // 动画执行时间
      duration: 4000,
      // 线的纹理宽度
      iconWidth: 10,
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
    
    // 若希望 2 秒后停止 polylineId 为 10 的轨迹动画，并将轨迹绘制完整。代码如下：
    setTimeout(() => {
          this.mapCtx.smoothMovePolyline({
            polylineId: 10,
            action: 'stop',
          });
    }, 2000);
  },
  // 动画结束的回调事件
  onPolylineMoveEnd(res)  {                                                      
    console.log('onPolylineMoveEnd: ' + JSON.stringify(res));         
  },
});
```

## 入参

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| polylineId | Number | 是 | 线 ID。 |
| points | Array | 是 | 经纬度数组，确定线。 |
| duration | Number | 否 | 绘制的时间，默认为 5000 毫秒（ms）。 |
| color | String | 否 | 线的颜色。默认透明色。 |
| width | Number | 否 | 线宽度。 |
| dottedLine | Boolean | 否 | 是否虚线。 |
| iconPath | String | 否 | 线的纹理地址。iconPath 引用图片宽高需要为 2 的整数次幂 |
| iconWidth | Number | 否 | 线的纹理宽度。设置 iconPath 后生效 |
| zIndex | Number | 否 | 线的层级，zIndex 数值高的线覆盖在低的上面 |
| colorList | Array | 否 | 彩虹线。如：`colorList:['#ff0000']` 。iOS 上暂不支持 colorList 功能|
| action | String | 否 | 指定操作动画。<ul><li>`action:'stop'` 表示在画线过程中提前停止动画，并将轨迹绘制完整。</li><li>`action:'start'` 默认值，表示执行动画。</li></ul> |
| success | Function | 否 | 参数校验成功的回调函数。 |
| fail | Function | 否 | 参数校验失败的回调函数。 |
| complete | Function | 否 |调用结束的回调函数（调用成功、失败都会执行）。 |

## 回调事件
 
回调事件需要在 map 中进行注册，js 中进行回调          

例：`<map onPolylineMoveEnd="onPolylineMoveEnd"></map>`                                                                                                            
| **回调事件**      | **类型** | **描述**             |
| ----------------- | -------- | -------------------- |
| onPolylineMoveEnd | Function | 动画结束的回调事件。 |

## 错误码

| **错误码**       | **说明** | **解决方案**                            |
| -------------- | -------- | ----------------------------------- |
| 2          | 限安卓环境。points 参数错误   | points 数组长度需要大于等于 2 |
| 10001          | 限 iOS 环境。未指定 polylineId   | 请给 polylineId 赋值 |

# 常见问题 FAQ

## Q：在地图上使用 MapContext.smoothMovePolyline 生成的轨迹线路为什么无法使用 clearRoute 清除？

A：clearRoute 只能用于清除地图上的导航路线，无法清除 MapContext.smoothMovePolyline 生成的线。请使用 MapContext.updateComponents 清除 示例如下：
```javascript
 this.mapCtx = my.createMapContext('map');

 //清除所有线路，代码如下：
 this.mapCtx.updateComponents({ polyline:[] }) 

 // map 上只保留 aniPoints 定义的线路，代码如下：
 this.mapCtx.updateComponents({
    polyline: [{
      points: aniPoints,
      color: '#0000FF',
      width: 10,
    }],
 })

```
