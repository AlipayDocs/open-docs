# 简介

**MapContext.showRoute** 需要开发者提供起点和终点的经纬度，系统会在两点间选取一条规划路线展示在地图上。

支付宝客户端 10.1.50 及以上版本支持规划步行、公交、骑行和驾车四种路线。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器暂不支持获取返回值，请使用真机预览获取返回值。
- 目前步行最多支持 100 公里的规划路线。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码

```html
//.axml
<map
  id="map"
  customMapStyle="light"
  onCalloutTap="callouttap"
  show-location
  style="width: 100%; height: 200px;"
  include-points="{{includePoints}}"
>
</map>
```

### .js 示例代码

```javascript
//.js
Page({
  onReady() {
    // 使用 my.createMapContext 获取 map 上下文
    this.mapCtx.showRoute({
      searchType: 'walk', // 搜索类型：10.1.50新增，有"walk", "bus", "drive", "ride", 默认值为walk
      startLat: 30.257839, // 起点纬度
      startLng: 120.062726, // 起点经度
      endLat: 30.256718, // 终点纬度
      endLng: 120.059985, // 终点经度
      throughPoints: [
        { lat: 39.866958, lng: 116.494231 },
        { lat: 39.9357, lng: 116.581092 },
      ], //途径点：10.1.50新增,仅驾车规划有效，searchType=“drive”
      routeColor: '#FFB90F', // 路线颜色  10.1.50之后，该值仅在2d地图中生效
      iconWidth: 10, // 纹理宽度  10.1.35 iconPath设置时才生效。10.1.50建议不再设置，在3d地图下提供了默认的纹理宽度。
      routeWidth: 10, // 路线宽度  在不设置纹理时有效。 10.1.50建议不再设置，在2d地图下提供了默认值，3d不需要设置。
      zIndex: 4, // 覆盖物 Z 轴坐标  10.1.35
      mode: 0, // 只有驾车模式和公交模式支持，可选,具体值见下表
      city: 'hangzhou', // 公交模式下必填
      destinationCity: 'hangzhou', // 公交跨城模式下必填
      success: function (res) {
        console.log(res, 'showRoute 执行结果：' + res.success  + '.总路程:' + res.distance + '米,需要时间' + res.duration + '秒');
      },
    });
  },
  onLoad() {
    this.mapCtx = my.createMapContext('map');
    this.setData({
      includePoints: [
        {
          latitude: 30.257839,
          longitude: 120.062726,
        },
        {
          latitude: 30.256718,
          longitude: 120.059985,
        },
      ],
    });
  },
});
```

## 返回示例

### success 返回示例

执行成功时，触发 success 回调，回调参数示例如下：

```json
{
  "distance": 328,
  "duration": 262,
  "success": true
}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| searchType | String | 否 | 搜索类型。<br />可选值：<ul><li>walk：步行。</li><li>bus：公交。</li><li>drive：驾车。</li><li>ride：骑行。</li></ul>默认值为 `walk`。<br />基础库 1.13.0 或更高版本开始支持。 |
| startLat | Number | 是 | 起点纬度。 |
| startLng | Number | 是 | 起点经度。 |
| endLat | Number | 是 | 终点纬度。 |
| endLng | Number | 是 | 终点经度。 |
| throughPoints | Array | 否 | 途径点，仅驾车规划有效，即 searchType=“drive” 时有效。<br />基础库 1.13.0 或更高版本开始支持。 |
| routeColor | HexColor | 否 | 路线颜色，该值仅在 2D 地图中生效。<br />基础库 1.13.0 或更高版本开始支持。 |
| iconPath | String | 否 | 路线纹理。<br />基础库 1.11.0 及以下版本中，3D 地图中该参数优先级高于 routeColor，即纹理会覆盖颜色值。<br />基础库 1.13.0 及以上版本建议不设置该参数，因为在 3D 地图下提供了默认的纹理图案，图片尺寸建议为 2 的整数幂，例如 64\*64。 |
| iconWidth | Int | 否 | 纹理宽度。<br />基础库 1.11.0 及以下版本中，该参数才生效。<br />基础库 1.13.0 及以上版本建议不设置该参数，因为在 3D 地图下提供了默认的纹理宽度。 |
| routeWidth | Int | 否 | 路线宽度。在不设置纹理时有效。<br />基础库 1.13.0 及以上版本建议不再设置，在 2D 地图下提供了默认值，3D 地图下不需要设置。 |
| zIndex | Int | 否 | 覆盖物的 Z 轴坐标。<br />基础库 1.11.0 或更高版本开始支持。 |
| mode | Int | 否 | 仅在驾车模式和公交模式支持，具体值见 **Int mode**。 |
| city | String | 是 | 公交模式下必填 。 |
| destinationCity | String | 是 | 公交跨城模式下必填。 |
| success | Function | 否 | 调用成功的回调函数。 |

### Int mode

| **mode** | **bus** | **drive** |
| --- | --- | --- |
| 0 | 最快捷模式 | 速度优先（时间）。 |
| 1 | 最经济模式 | 费用优先（不走收费路段的最快道路）。 |
| 2 | 最少换乘模式 | 距离优先。 |
| 3 | 最少步行模式 | 不走快速路。 |
| 4 | 最舒适模式 | 结合实时交通（躲避拥堵）。 |
| 5 | 不乘地铁模式 | 多策略（同时使用速度优先、费用优先、距离优先三个策略）。 |
| 6 | - | 不走高速。 |
| 7 | - | 不走高速且避免收费。 |
| 8 | - | 躲避收费和拥堵。 |
| 9 | - | 不走高速且躲避收费和拥堵。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**         |
| -------- | -------- | ---------------- |
| success  | Boolean  | 是否成功。       |
| distance | Number   | 距离，单位为米。 |
| duration | Number   | 时间，单位为秒。 |


## 错误码

| **错误码** | **描述**       | **解决方案**                               |
| ---------- | -------------- | ------------------------------------------ |
| 3003/60001/30007        | 步行/公交/骑行起点终点经纬度差距过大，路线规划失败 | 缩小经纬度差距 |
