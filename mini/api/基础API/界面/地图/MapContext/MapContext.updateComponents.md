
# 简介
**MapContext.updateComponents** 是增量更新地图的接口。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.updateComponents({
    scale: 14,
    longitude: 120.131441,
    latitude: 30.279383,
    command:{                                   
        // marker动画
        markerAnim:[
            {
                type:0           // 跳动动画 10.1.35
                markerId:xxx,
            }
        ],     
    },
    setting:{
        // 手势
        gestureEnable:0/1,
        // 比例尺
        showScale:0/1,
        // 指南针
        showCompass:0/1,
        // 双手下滑
        tiltGesturesEnabled:0/1,
        // 交通路况展示
        trafficEnabled:0/1,                     
        // 地图POI信息
        showMapText:0/1, 
        // 高德地图logo位置
        logoPosition:{centerX:150, centerY:90},                       
    },
    markers:[{},{}],
    polyline:[{},{}],
    include-points:[{},{}],
    include-padding:{left:0, right:0, top:0, bottom:0},
});
```

## 入参
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| latitude | Number | 中心纬度。 |
| longitude | Number | 中心经度。 |
| scale | Number | 缩放级别，取值范围为 5-18。默认值为 16。 |
| markers | Array | 覆盖物，在地图上的一个点绘制图标。 |
| polyline | Array | 覆盖物，多个连贯点的集合（路线）。 |
| include-points | Array | 视野将进行小范围延伸包含传入的坐标。 |
| include-padding | Object | 视野在地图 padding 范围内展示。 |
| setting | Object | 设置。 |
| command | Object | 命令，可用于更新 marker 动画。 |

