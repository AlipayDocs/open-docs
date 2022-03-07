
# 简介
**MapContext.calculateDistance** 计算途经地图上多个点的路径长度，并可按指定距离截取该路径。

例如：入参 { points: [A, B, C]，targetDistances: [d1, d2] }，success 回调的参数 { distance, targetPoints: [X, Y] } <br>用 dist(M, N) 代表坐标 M 到 N 的直线距离，则有 distance == dist(A, B) + dist(B, C)<br>若 0 <= d1 < dist(A, B)，则 X 在线段 AB 上（X.targetLineIndex == 0），且 dist(A, X) == d1<br>若 0 <= d2 - dist(A, B) < dist(B, C)，则 Y 在线段 BC 上（Y.targetLineIndex == 1），且 dist(A, B) + dist(B, Y) == d2

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端版本 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器暂不支持模拟，请以真机调试效果为准。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js

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

this.mapCtx.calculateDistance({
      points:aniPoints,
      targetDistances:[100,200,300,600],
      success: (res) => {
          my.alert({ content: 'calculateDistance: ' + JSON.stringify(res), });
      },
})
```


## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| points | Array | 是 | 顺序排列的路径节点数组。每个节点形如 { latitude, longitude } |
| exportTotalDistance | Boolean | 否 | 是否需要计算路径总长度，默认为 true。 |
| targetDistances | Array | 否 | 目标路径长度数组。<br>如有提供，接口将按这些长度截取子路径（以 points[0] 为起点），终点作为出参 targetPoints 的元素 |


### success 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| distance | Number | 路径总长度。如果传入的 exportTotalDistance 为 false，则不返回 distance。
| targetPoints | Array | 按 targetDistances 截取的子路径的终点。<br />每个点的属性参见下方 **targetPoint 对象**。 |


### targetPoint 对象
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| latitude | Number | 纬度。 |
| longitude | Number | 经度。 |
| index | Number | 此 targetPoint 对应的 targetDistances 索引。<br>targetPoints 会按所截子路径长度升序排列，与 targetDistances 顺序可能不同 |
| targetDistance | Number | 此 targetPoint 截取的子路径的长度。值为 targetDistances[index]。 |
| targetLineIndex | Number | 此 targetPoint 所在线段的索引。<br>入参 points 中每一对相邻元素构成一条线端，每 i 条线段的端点为 points[i] 和 points[i + 1] |


## 返回值示例代码
```json
{"distance":0,"success":true,"targetPoints":
[{"index":0,"latitude":30.261775,"longitude":120.102507,"targetDistance":100,"targetLineIndex":0},
{"index":1,"latitude":30.261775,"longitude":120.102507,"targetDistance":200,"targetLineIndex":0},
{"index":2,"latitude":30.261775,"longitude":120.102507,"targetDistance":300,"targetLineIndex":0},
{"index":3,"latitude":30.261775,"longitude":120.102507,"targetDistance":600,"targetLineIndex":0}]
}
```
