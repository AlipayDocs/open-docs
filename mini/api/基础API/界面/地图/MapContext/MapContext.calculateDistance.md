# 简介

**MapContext.calculateDistance** 计算由一系列坐标点所定义的路径的长度，并可计算出该路径上距起始点指定距离的点的坐标。

例如：入参 { points: [A, B, C]，targetDistances: [d1, d2] }<br>success 回调的参数 { distance: distance, targetPoints: [X, Y] } <br><br>ABC 三点确定由两段直线（AB， BC）组成的路径，distance 等于路径的总长（单位米）<br>沿着这条路径距离 A 点 d1 长度的即为目标点 X ，d2 长度的就是目标点 Y。

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端版本 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js

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

this.mapCtx.calculateDistance({
  points: aniPoints,
  targetDistances: [100, 200, 300, 600],
  success: res => {
    my.alert({ content: 'calculateDistance: ' + JSON.stringify(res) });
  },
});
```

## 入参

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| points | Array | 是 | 顺序排列的路径节点数组，第一个点为起点。<br>每个节点形如 { latitude, longitude } |
| exportTotalDistance | Boolean | 否 | 是否需要计算路径总长度（单位米），默认为 true。 |
| targetDistances | Array | 否 | 目标距离数组。<br>如提供，接口将按其中每个目标距离（单位米）计算出路径上的目标点，放到出参的 targetPoints 数组 |

### success 返回值

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| distance | Number | 由入参 points 中的点所定义的路径总长度（相邻点的直线距离逐段累加）。单位米<br>如果传入的 exportTotalDistance 为 false，则不返回 distance。 |
| targetPoints | Array | 按入参 targetDistances 所计算出的目标点。<br />每个点的属性参见下方 **targetPoint 对象**。 |

### targetPoint 对象

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| latitude | Number | 纬度。 |
| longitude | Number | 经度。 |
| targetDistance | Number | 从起点到此目标点的路径长度（单位米）。 |
| index | Number | 值等于 targetDistance 对应 targetDistances 中的对应项的索引。 |
| targetLineIndex | Number | 此目标点所在线段的索引。<br>第 i 条线段的索引值为 i - 1 |

## 返回值示例代码

```json
{
  "distance": 0,
  "success": true,
  "targetPoints": [
    {
      "index": 0,
      "latitude": 30.261775,
      "longitude": 120.102507,
      "targetDistance": 100,
      "targetLineIndex": 0
    },
    {
      "index": 1,
      "latitude": 30.261775,
      "longitude": 120.102507,
      "targetDistance": 200,
      "targetLineIndex": 0
    },
    {
      "index": 2,
      "latitude": 30.261775,
      "longitude": 120.102507,
      "targetDistance": 300,
      "targetLineIndex": 0
    },
    {
      "index": 3,
      "latitude": 30.261775,
      "longitude": 120.102507,
      "targetDistance": 600,
      "targetLineIndex": 0
    }
  ]
}
```
