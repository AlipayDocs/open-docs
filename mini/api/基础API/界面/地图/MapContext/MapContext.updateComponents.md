# 简介

**MapContext.updateComponents** 设置地图属性及覆盖物。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
this.mapCtx = my.createMapContext('map');
this.mapCtx.updateComponents({
  scale: 15, // 缩放级别
  longitude: 120.125872, // 中心经度
  latitude: 30.272960, // 中心纬度
  command: {
    // marker 动画
    markerAnim: [
      { type: 1, markerId: 1 },
      { type: 1, markerId: 2 },
    ],
  },
  setting: {
    gestureEnable: 1, // 开启手势功能
    showScale: 1, // 显示比例尺
    showCompass: 1, // 显示指南针
    tiltGesturesEnabled: 1, // 开启双指下滑手势
    trafficEnabled: 1, // 显示交通路况
    showMapText: 1, // 显示地图 POI 信息
    logoPosition: { centerX: 150, centerY: 90 }, // 指定地图 logo 位置
  },
  // 点标记覆盖物
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
  // 线段覆盖物
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
  // 包含点
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
  // 内边距
  'include-padding': {
    left: 10,
    right: 0,
    top: 0,
    bottom: 0
  },
  // 贴图覆盖物
  'ground-overlays':[{
    // 刷新的时候需要变更id值
    id:'10', 
    // 确定贴图覆盖物位置
    'include-points':[{
        latitude: 39.935029,
        longitude: 116.384377,
    },{
        latitude: 39.939577,
        longitude: 116.388331,
    }],
    image: 'https://gw.alipayobjects.com/mdn/rms_dfc0fe/afts/img/A*x9yERpemTRsAAAAAAAAAAAAAARQnAQ',
  }],
  success: res => {
    console.log('res', res);
  },
  fail: res => {
    console.log('fail', res);
  }
});
```

## 入参

| **属性**        | **类型** | **必填** | **描述**                                                                                         |
| --------------- | -------- | -------- | ------------------------------------------------------------------------------------------------ |
| latitude        | Number   | 否       | 中心纬度。                                                                                       |
| longitude       | Number   | 否       | 中心经度。                                                                                       |
| scale           | Number   | 否       | 缩放级别，取值范围为 5-18。默认值为 16。                                                         |
| markers         | Array    | 否       | 点标记覆盖物数组。格式详见 [markers](https://opendocs.alipay.com/mini/component/map#markers)  。 |
| polyline        | Array    | 否       | 线段覆盖物数组。格式详见 [polyline](https://opendocs.alipay.com/mini/component/map#polyline)。   |
| include-points  | Array    | 否       | 包含点。地图的可视区域将至少包含这些点。                                                         |
| include-padding | Object   | 否       | 内边距。设置由 include-points 确定的可视区域与地图的内边距。详见 **Object include-padding**      |
| ground-overlays | Array&lt;Object&gt;    | 否       | 贴图覆盖物。详见 **Array ground-overlays**                                                
| setting         | Object   | 否       | 地图设置，如手势功能/地图信息等。详见 **Object setting**                                         |
| command         | Object   | 否       | 命令。目前仅支持 markerAnim（标记点动画）。详见 **Object command**                               |

### Object include-padding
| **属性** | **类型** | **必填** | **描述** |
| -------- | -------- | -------- | -------- |
| left     | Number   | 是       | 左内边距 |
| right    | Number   | 是       | 右内边距 |
| top      | Number   | 是       | 上内边距 |
| bottom   | Number   | 是       | 下内边距 |

### Array&lt;Object&gt; ground-overlays
每个数组元素包含如下属性：
| **属性** | **类型** | **必填** | **描述** |
| -------- | -------- | -------- | -------- |
| id     | String   | 否      | 覆盖物 id。用于刷新指定贴图覆盖物。 |
| include-points  | Array    | 否       | 包含点。用于确定贴图覆盖物位置。                   |
| image      | String   | 否       | 贴图覆盖物图片的路径 |
| alpha   | Number   | 否      | 贴图覆盖物不透明度。默认为 1。 |
| zIndex   | Number   | 否      | 设置贴图覆盖物层级。 |


### Object setting
| **属性**            | **类型** | **必填** | **描述**                                                                        |
| ------------------- | -------- | -------- | ------------------------------------------------------------------------------- |
| gestureEnable       | Number   | 否       | 是否开启手势功能（可旋转地图）。默认值为 1。                                    |
| showScale           | Number   | 否       | 是否显示比例尺。1 显示，0 不显示。默认值为 1。                                  |
| showCompass         | Number   | 否       | 是否显示指南针。1 显示，0 不显示。默认值为 1。                                  |
| tiltGesturesEnabled | Number   | 否       | 是否双指滑动功能（可修改地图倾斜角）。1 开启，0 不开启。默认值为 0。            |
| trafficEnabled      | Number   | 否       | 是否显示交通路况。1 显示，0 不显示。默认值为 1。                                |
| showMapText         | Number   | 否       | 是否显示 POI 信息，如商店、加油站、医院、车站等。1 显示，0 不显示。默认值为 1。 |
| logoPosition        | Object   | 否       | 设置地图 logo 位置。详见 **Object logoPosition**                                |

#### Object logoPosition
| **属性** | **类型** | **必填** | **描述**      |
| -------- | -------- | -------- | ------------- |
| centerX  | Number   | 是       | 屏幕 X 轴坐标 |
| centerY  | Number   | 是       | 屏幕 Y 轴坐标 |

### Object command
| **属性**   | **类型**            | **必填** | **描述**                                                                       |
| ---------- | ------------------- | -------- | ------------------------------------------------------------------------------ |
| markerAnim | Array&lt;Object&gt; | 否       | marker 动画数组，可同时设置多个 marker 动画。参见 **Array<Object> markerAnim** |

#### Array&lt;Object&gt; markerAnim
每个数组元素包含如下属性：
| **属性** | **类型** | **必填** | **描述**                                |
| -------- | -------- | -------- | --------------------------------------- |
| markerId | Number   | 是       | 执行动画的标记点 id                     |
| type     | Number   | 是       | 动画类型，目前仅支持跳动动画（type = 1) |
