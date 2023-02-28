# 简介

**MapContext.smoothMovePolyline** 绘制折线，产生轨迹动画。

也可使用此 API 结束进行中的绘制动画（入参 action 字段传 'stop'）。

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
  <view onTap="smoothMovePolyline">绘制折线</view>
</view>
```

```javascript
// .js
Page({
  smoothMovePolyline() {
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
      // 折线 id
      polylineId: 10,
      // 经纬度数组，指定绘制路径
      points: aniPoints,
      // 线路颜色
      color: '#00FF00',
      // 线路宽度
      width: 10,
      // 是否虚线
      dottedLine: false,
      // 动画执行时间
      duration: 4000,
      success: res => {
        console.log('success' + JSON.stringify(res))
      },
      fail: err => {
        console.log('err' + JSON.stringify(err))
      },
      complete: res => {
        console.log('complete' + JSON.stringify(res))
      }
    });

    setTimeout(() => {
      this.mapCtx.smoothMovePolyline({
        polylineId: 10,
        action: 'stop', // 停止动画（直接完成折线绘制）
      });
    }, 2000);
  },
  onPolylineMoveEnd(res) {
    console.log('onPolylineMoveEnd: ' + JSON.stringify(res));
  },
});
```

## 入参

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| polylineId | Number | 是 | 折线 id。 |
| points | Array\<Object\> | 是 | 经纬度数组，确定绘制的折线。数组每个元素应包含 latitude 和 longitude 属性。 |
| duration | Number | 否 | 绘制的时间，默认为 5000，单位毫秒。 |
| color | String | 否 | 折线颜色。默认为透明色。 |
| width | Number | 否 | 折线宽度。默值为 0。 |
| dottedLine | Boolean | 否 | 是否设置虚线。默值为 false。 |
| iconPath | String | 否 | 折线纹理地址。iconPath 引用图片宽高需要为 2 的整数次幂 |
| iconWidth | Number | 否 | 折线纹理宽度。设置 iconPath 后生效 |
| zIndex | Number | 否 | 折线的层级。 |
| colorList | Array | 否 | 折线的各段颜色。长度为 points.length - 1。例：`colorList:['#ff0000']` 。iOS 上暂不支持 colorList 功能。|
| action | String | 否 | 操作类型。'start'（默认值）表示开始移动。'stop' 表示结束绘制动画，折线直接绘制完成。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 |调用结束的回调函数（调用成功、失败都会执行）。 |

## 事件回调
折线绘制完成时会触发 onPolylineMoveEnd 事件。需通过 map 组件注册其回调函数，如：`<map onPolylineMoveEnd="polylineEnd"></map>`  

## 错误码

| **错误码**       | **说明** | **解决方案**                            |
| -------------- | -------- | ----------------------------------- |
| 2          | 参数错误   | points 数组长度需要大于 1 |
| 10001          | 缺少 polylineId   | 传入 polylineId 值 |

# 常见问题 FAQ

## Q：在地图上使用 MapContext.smoothMovePolyline 生成的轨迹为什么无法使用 clearRoute 清除？

A：clearRoute 只能用于清除地图上的导航路线（route），smoothMovePolyline 产生的轨迹是折线（polyline），需要使用 MapContext.updateComponents 设置：
```javascript
 this.mapCtx = my.createMapContext('map');

 // 清除地图上所有折线
 this.mapCtx.updateComponents({ polyline:[] }) 

 // 地图只显示一条折线 (由 aniPoints 定义）
 this.mapCtx.updateComponents({
    polyline: [{
      points: aniPoints,
      color: '#0000FF',
      width: 10,
    }],
 })

```
