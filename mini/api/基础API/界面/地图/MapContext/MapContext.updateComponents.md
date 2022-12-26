# 简介

**MapContext.updateComponents** 是更新[地图](https://opendocs.alipay.com/mini/component/map#)属性的接口。地图属性包含中心经纬度、缩放级别、点标记、线段覆盖物、可视区域等。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.updateComponents({
  // 缩放级别
  scale: 15,
  // 经度
  longitude: 120.125872,
  // 纬度
  latitude: 30.272960,
  // 动画命令
  command: {
    // marker 动画
    markerAnim: [
      {
        type: 1, 
        markerId: 1,
      },
      {
        type: 1, 
        markerId: 2,
      },
    ],
  },
  setting: {
    // 手势
    gestureEnable: 1, // 0 或 1
    // 比例尺
    showScale: 1, //  0 或 1
    // 指南针
    showCompass: 1, // 0 或 1
    // 双手下滑
    tiltGesturesEnabled: 1, // 0 或 1
    // 交通路况展示
    trafficEnabled: 1, // 0 或 1
    // 地图 POI 信息
    showMapText: 1, //  0 或 1
    // 地图 logo 位置
    logoPosition: {
      centerX: 150,
      centerY: 90
    },
  },
  // 点标记覆盖物数组
  markers: [
    {
      id: 1,
      latitude: 30.272960,
      longitude: 120.125872,
      width: 19,
      height: 31,
      iconPath: 'https://gw.alipayobjects.com/mdn/rms_dfc0fe/afts/img/A*x9yERpemTRsAAAAAAAAAAAAAARQnAQ',
      callout: {
        content: '1',
      },
    }, 
    {
      id: 2,
      latitude: 30.275960,
      longitude: 120.125872,
      width: 19,
      height: 31,
      iconPath: 'https://gw.alipayobjects.com/mdn/rms_dfc0fe/afts/img/A*x9yERpemTRsAAAAAAAAAAAAAARQnAQ',
      callout: {
        content: '2',
      },
    }
  ],
  // 线段覆盖物数组
  polyline: [
    {
      points: [
        {
          latitude: 30.272960,
          longitude: 120.125872,
        }, 
        {
          latitude: 30.272960,
          longitude: 120.124572,
        },
        {
          latitude: 30.274260,
          longitude: 120.124572,
        }
      ],
      color: '#FF0000DD',
      width: 10,
      dottedLine: false,
      iconWidth: 10,
    }
  ],
  // 将传入的经纬度数组全部显示在视野中
  'include-points': [
    {
      latitude: 30.272960,
      longitude: 120.125872,
    },
    {
      latitude: 30.275960,
      longitude: 120.125872,
    },
  ],
  'include-padding': { left: 10, right: 0, top: 0, bottom: 0 },
  success: res => {
    console.log('res', res);
  },
  fail: res => {
    console.log('fail', res);
  }
});
```

## 入参

| **属性**        | **类型** | **必填** | **描述**                                 |
| --------------- | -------- | -------- | ---------------------------------------- |
| latitude        | Number  | 否| 中心纬度。                               |
| longitude       | Number    | 否| 中心经度。                               |
| scale           | Number    | 否| 缩放级别，取值范围为 5-18。默认值为 16。 |
| markers         | Array     | 否| 点标记覆盖物数组。格式详见 [markers](https://opendocs.alipay.com/mini/component/map#markers)  。      |
| polyline        | Array     | 否| 线段覆盖物数组。格式详见 [polyline](https://opendocs.alipay.com/mini/component/map#polyline)。 |
| include-points  | Array     | 否| 经纬度数组。移动缩放地图，将传入的经纬度数组全部显示在可视区域中。     |
| include-padding | Object    | 否| 设置由 include-points 确定的可视区域与地图的内边距。详情见 **Object include-padding**          |
| setting         | Object   | 否 | 打开手势功能，显示地图信息。详情见 **Object setting**   |
| command         | Object    | 否| 输入命令。目前仅支持 markerAnim，详情见 **Object command** |

### Object include-padding
| **属性**        | **类型** | **必填** | **描述**                                 |
| --------------- | -------- | -------- |---------------------------------------- |
| left            | Number   |   是   | 左内边距 |
| right            | Number   |   是   | 右内边距 |
| top            | Number   |   是   | 上内边距 |
| bottom            | Number   |   是   | 下内边距 |

### Object setting
| **属性**        | **类型** | **必填** | **描述**                                 |
| --------------- | -------- | -------- |---------------------------------------- |
| gestureEnable            | Number   |   否   | 地图手势功能，可旋转地图。 |
| showScale            | Number   |   否   | 显示比例尺 |
| showCompass            | Number   |   否   | 显示指南针 |
| tiltGesturesEnabled            | Number   |   否   | 双指滑动功能，可修改地图倾斜角。 |
| trafficEnabled            | Number   |   否   | 显示交通路况 |
| showMapText            | Number   |   否   | 地图 POI 信息，如商店、加油站、医院、车站等 |
| logoPosition            | Object   |   否   | 地图 logo 位置。 详情见 **Object logoPosition** |

#### Object logoPosition
| **属性**        | **类型** | **必填** | **描述**                                 |
| --------------- | -------- | -------- |---------------------------------------- |
| centerX            | Number   |   是   | 屏幕 X 轴坐标 |
| centerY            | Number   |   是   | 屏幕 Y 轴坐标 |

### Object command
| **属性**        | **类型** | **必填** | **描述**                                 |
| --------------- | -------- | -------- |---------------------------------------- |
| markerAnim            | Array   |   否   | marker 动画数组，可同时设置多个 marker 动画。详情见 **Array markerAnim** |

#### Array markerAnim
| **属性**        | **类型** | **必填** | **描述**                                 |
| --------------- | -------- | -------- |---------------------------------------- |
| type            | Number   |   是   | 动画类型，目前仅支持跳动动画 。<ul><li>`type : 1` </li></ul> |
| markerId            | Number   |   是   | 需要执行动画的点标记 id               |
