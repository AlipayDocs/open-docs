# 简介

**my.calculateRoute** 是计算路径 API。根据起点和终点的地理位置，智能规划最佳出行路线，并计算不同出行方式下的行动距离和所需时间。

默认规划步行路线，支持规划步行、公交、骑行和驾车四种路线。

## 使用限制

- 基础库 [1.21.0](https://opendocs.alipay.com/mini/framework/lib)  或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
my.calculateRoute({
  searchType:"bus",                // 搜索类型："walk", "bus", "drive", "ride", 默认值为walk
  startLat:30.257839,              // 起点纬度
  startLng:120.062726,             // 起点经度
  endLat:30.256718,                // 终点纬度
  endLng:120.059985,               // 终点经度
  throughPoints:[{lat: 39.866958,lng:116.494231},{lat: 39.9357,lng:116.581092}],//途径点,仅驾车规划有效，searchType=“drive”
  mode:0,                          // 只有驾车模式和公交模式支持，可选，具体值见 mode 参数列表
  city:'hangzhou',                 // 公交模式下必填
  destinationCity:'hangzhou',      // 公交跨城模式下必填
  success:(e)=>{
    console.log(e.distance);
    console.log(e.duration);
    }
});
```

## 入参

Object 类型，参数如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| searchType | String | 否 | 搜索类型。<br />可选值：<ul><li>walk：步行。</li><li>bus：公交。</li><li>drive：驾车。</li><li>ride：骑行。</li></ul>默认值为 `walk`。 |
| startLat | Number | 是 | 起点纬度。 |
| startLng | Number | 是 | 起点经度。 |
| endLat | Number | 是 | 终点纬度。 |
| endLng | Number | 是 | 终点经度。 |
| throughPoints | Array | 否 | 途径点，仅驾车规划有效，即 searchType=“drive” 时有效。 |
| mode | Number | 否 | 仅在驾车模式和公交模式支持，具体值见 **Number mode**。 |
| city | String | 是 | 公交模式下必填。传参可填写城市中文名称或城市名称拼音。例如：`city:'hangzhou'` 或  `city:'杭州'`。 |
| destinationCity | String | 是 | 公交跨城模式下必填。 |
| success | Function | 否 | 调用成功的回调函数。 |

### Number mode
| **mode** | **模式** | **描述** |
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

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | 是否成功。成功返回 true，失败返回 false。 |
| distance | Number | 距离，单位为米。 |
| duration | Number | 时间，单位为秒。 |

## 错误码
错误码信息可查看：
- [Andriod 地图错误码对照表](https://lbs.amap.com/api/android-sdk/guide/map-tools/error-code)
- [iOS 地图错误码对照](https://lbs.amap.com/api/ios-sdk/guide/map-tool/errorcode/)

