
# 简介
同一个页面需要展示多个 map 组件的话，需要使用不同的 ID 。map 组件是由客户端创建的原生组件，原生组件的层级是最高的，所以页面中的其他组件无论设置 z-index 为多少，都无法在原生组件之上使用限制。

## 使用限制

- 支持高德地图 style 与火星坐标系。
- 支持通过同层渲染实现 [cover-view](https://opendocs.alipay.com/mini/component/cover-view) 覆盖 map 组件。同层渲染支持范围 10.1.35 及其以上版本 Android 的小程序，10.1.50 及其以上版本 iOS 的小程序。
- 不支持在 [scroll-view](https://opendocs.alipay.com/mini/component/scroll-view) 中使用 map 组件。
- 不支持使用 CSS  动画，CSS 动画对 map 组件无效。
- 缩小或者放大了地图比例尺之后，若再次设置 data 经纬度到一个地点，请在 onRegionChange 函数中重新设置 data 的 scale 值，否则会出现拖动地图区域后，重新加载导致地图比例尺又变回缩放前的大小，具体请参照示例代码 regionchange 函数部分。
- 基础库 [1.18.5](https://opendocs.alipay.com/mini/framework/lib) 开始支持 optimize 属性，开启 optimize 后，开发者不需要再监听 onRegionChange 来更新 scale 属性值以保证缩放比例不变。此特性在客户端 10.1.68 以上支持，可通过 [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use)（map.optimize）进行检测。

## 扫码体验
![|127x157](https://mdn.alipayobjects.com/afts/img/A*jE8JQpMNjY8BCY5OkWKVbABkAa8wAA/1024w_1024h_1l.jpg?bz=openpt_doc&t=le_fbHinaqYux4LacaqMEwAAAABkMK8AAAAA#align=left&display=inline&height=239&margin=%5Bobject%20Object%5D&originHeight=239&originWidth=193&status=done&style=none&width=193)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/p/OpenBox/use-doc-map?previewZoom=75)

## 示例代码

### .axml 示例代码
```html
<view>
  <map id="map" longitude="120.131441" latitude="30.279383" scale="{{scale}}" controls="{{controls}}"
  onControlTap="controltap" markers="{{markers}}"
  onMarkerTap="markertap"
  polyline="{{polyline}}" 
  circles="{{circles}}"
  panels="{{panels}}"
  onRegionChange="regionchange"
  onTap="tap"
  onPanelTap="onPanelTap"
  show-location style="width: 100%; height: 300px;"
  include-points="{{includePoints}}"></map>
  <button onTap="changeScale">改scale</button>
  <button onTap="getCenterLocation">getCenterLocation</button>
  <button onTap="moveToLocation">moveToLocation</button>
  <button onTap="changeCenter">改center</button>
  <button onTap="changeMarkers">改markers</button>
</view>
```

### .js 示例代码
```javascript
Page({
  data: {
    scale: 14,
    longitude: 120.131441,
    latitude: 30.279383,
    markers: [{
      iconPath: "/image/green_tri.png",
      id: 10,
      latitude: 30.279383,
      longitude: 120.131441,
      width: 50,
      height: 50
    },{
      iconPath: "/image/green_tri.png",
      id: 11,
      latitude: 30.279383,
      longitude: 120.131441,
      width: 50,
      height: 50,
      customCallout: {
        type: 1,
        time: '1',
      },
      fixedPoint:{
        originX: 400,
        originY: 400,
      },
      iconAppendStr: '黄龙时代广场黄龙时代广场黄龙时代广场黄龙时代广场test'
    }],
    includePoints: [{
      latitude: 30.279383,
      longitude: 120.131441,
    }],
    polyline: [{
      points: [{
        longitude: 120.131441,
        latitude: 30.279383
      }, {
        longitude: 120.128821,
        latitude: 30.278200
      }, {
        longitude: 120.131618,
        latitude: 30.277600
      }, {
        longitude: 120.132520,
        latitude: 30.279393
      }, {
        longitude: 120.137517,
        latitude: 30.279383
      }],
      color: "#FF0000DD",
      width: 5,
      dottedLine: false
    }],
    circles: [{
      latitude: 30.279383,
      longitude: 120.131441,
      color: "#000000AA",
      fillColor: "#000000AA",
      radius: 80,
      strokeWidth: 5,
    }],
    controls: [{
      id: 5,
      iconPath: '../../resources/pic/2.jpg',
      position: {
        left: 0,
        top: 300 - 50,
        width: 50,
        height: 50
      },
      clickable: true
    }],
    panels:[{
    	 id:6,
       // 布局参考 map 高级定制渲染
       layout: {
   			 	params:{
      			title:"标题栏",
      			bgColor:"#DC143C"
    			},
   		 		src:"/layout/map_callout.xml"
  		 },
       position: {
         left: 0,
         bottom: 0,
         width: 200,
         height: 84
       },
    }],
  },
  onReady(e) {
    // 使用 my.createMapContext 获取 map 上下文
    this.mapCtx = my.createMapContext('map')
  },
  getCenterLocation() {
    this.mapCtx.getCenterLocation(function (res) {
      console.log(res.longitude)
      console.log(res.latitude)
    })
  },
  moveToLocation() {
    this.mapCtx.moveToLocation()
  },
  regionchange(e) {
    console.log('regionchange', e);
	// 注意：如果缩小或者放大了地图比例尺以后，请在 onRegionChange 函数中重新设置 data 的
	// scale 值，否则会出现拖动地图区域后，重新加载导致地图比例尺又变回缩放前的大小。
	if (e.type === 'end') {
      this.setData({
        scale: e.scale
      });
    }
  },
  markertap(e) {
    console.log('marker tap', e);
  },
  controltap(e) {
    console.log('control tap', e);
  },
  tap() {
    console.log('tap:');
  },
  onPanelTap(e) {
    console.log('paneltap:', e);
  },
  changeScale() {
    this.setData({
      scale: 8,
    });
  },
  changeCenter() {
    this.setData({
      longitude: 113.324520,
      latitude: 23.199994,
      includePoints: [{
        latitude: 23.199994,
        longitude: 113.324520,
      }],
    });
  },
  //支持地图不接受手势事件, isGestureEnable为1 表示支持，为0表示不支持
  gestureEnable() {
    this.mapCtx.gestureEnable({isGestureEnable:1});
  },
  
//地图是否显示比例尺, isShowsScale 为1表示显示，为0表示不显示
  showsScale() {
    this.mapCtx.showsScale({isShowsScale:1});
  },
  //地图是否显示指南针, isShowsCompass 为1表示显示，为0表示不显示
  showsCompass() {
    this.mapCtx.showsCompass({isShowsCompass:1});
  },
  changeMarkers() {
    this.setData({
      markers: [{
        iconPath: "/image/green_tri.png",
        id: 10,
        latitude: 21.21229,
        longitude: 113.324520,
        width: 50,
        height: 50
      }],
      includePoints: [{
        latitude: 21.21229,
        longitude: 113.324520,
      }],
    });
  },
})
```

## 属性说明
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| style | String | 内联样式 。 |
| class | String | 样式名 。 |
| latitude | Number | 中心纬度。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| longitude | Number | 中心经度。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| scale | Number | 缩放级别，取值范围为 5-18 。<br />**默认值：** 16<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| skew | Number | 倾斜角度，范围 0 ~ 40 , 关于 z 轴的倾角。<br />**默认值：** 0<br />**版本要求：** 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| rotate | Number | 顺时针旋转的角度，范围 0 ~ 360。<br />**默认值：** 0<br />**版本要求：** 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| markers | Array | 覆盖物，在地图上的一个点绘制图标。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| polyline | Array | 覆盖物，多个连贯点的集合（路线）。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| circles | Array | 覆盖物，圆。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| controls | Array | 在地图 View 之上的一个控件。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| polygon | Array | 覆盖物，多边形。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| show-location | Boolean | 是否显示带有方向的当前定位点。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| include-points | Array | 视野将进行小范围延伸包含传入的坐标。<br />[{<br />    latitude: 30.279383,<br />    longitude: 120.131441,<br />}]<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| include-padding | Object | 视野在地图 padding 范围内展示。<br />{<br />    left:0, right:0,<br />    top:0, bottom:0<br />}<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| ground-overlays | Array | 覆盖物，自定义贴图。<br />[{<br />    // 刷新的时候需要变更id值<br />    id:'0', <br />    // 右上，左下<br />    'include-points':[{<br />        latitude: 39.935029,<br />        longitude: 116.384377,<br />    },{<br />        latitude: 39.939577,<br />        longitude: 116.388331,<br />    }],<br />    image:'/image/overlay.png',<br />    alpha:0.25,<br />    zIndex:1<br />}]<br />**版本要求：** 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| tile-overlay | Object | 覆盖物，网格贴图。<br />{<br />    url:'http://xxx',<br />    type:0, // url类型<br />    tileWidth:256,<br />    tileHeight:256,<br />    zIndex:1,<br />}<br />**版本要求：** 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| custom-map-style | String | 设置地图样式。 default：默认样式<br />light：精简样式<br />**版本要求：** 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| panels | Array | 基于 [map 高级定制渲染](https://opendocs.alipay.com/mini/00n21l)，设置覆盖在地图上的 view。<br />**版本要求**：基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| setting | Object | 设置。<br />{<br />  // 手势<br />  gestureEnable: 1,<br />  // 比例尺<br />  showScale: 1,<br />  // 指南针<br />  showCompass: 1,<br />  //双手下滑<br />  tiltGesturesEnabled: 1,<br />  // 交通路况展示<br />  trafficEnabled: 0,<br />  // 地图 POI 信息<br />  showMapText: 0,<br />  // 高德地图 logo 位置<br />  logoPosition: {<br />    centerX: 150,<br />    centerY: 90<br />  }<br />} |
| onMarkerTap | EventHandle | 点击 Marker 时触发。<br />{<br />    markerId,<br />    latitude,<br />    longitude, <br />}<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| onCalloutTap | EventHandle | 点击 Marker 对应的 callout 时触发。<br />{<br />    markerId,<br />    latitude,<br />    longitude, <br />}<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| onControlTap | EventHandle | 点击 control 时触发。<br />{<br />    controlId<br />}<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| onRegionChange | EventHandle | 视野发生变化时触发。<br />基础库 1.24.0 版本新增 skew、rotate、causedBy 返回；<br />begin 阶段 causedBy 有效值为 update(接口触发)、gesture(手势触发)；<br />end 阶段 causedBy 有效值为 update(接口触发)、drag/scale/skew/rotate (手势触发)。<br />{<br />    type: "begin/end", <br />    latitude,<br />    longitude, <br />    scale,<br />    skew,<br />    rotate,<br />    causedBy: "update/gesture"<br />}<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| onTap | EventHandle | 点击地图时触发。<br />{<br />    latitude,<br />    longitude, <br />}<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| onPanelTap | EventHandle | 点击 panel 时触发。<br />{ <br />   panelId,<br />   layoutId,<br />}<br />**版本要求：** 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| show-compass | Boolean | 显示指南针。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| show-scale | Boolean | 显示比例尺。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| enable-overlooking | Boolean | 开启俯视。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| enable-zoom | Boolean | 是否支持缩放。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| enable-scroll | Boolean | 是否支持拖动。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| enable-rotate | Boolean | 是否支持旋转。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| enable-traffic | Boolean | 是否开启实时路况。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| enable-poi | Boolean | 是否展示 POI 点。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| enable-building | Boolean | 是否展示建筑物。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onInitComplete | EventHandle | 地图初始化完成即将开始渲染第一帧时触发。<br />**版本要求**：基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |


### markers

#### 简介
标记点，用于在地图上显示标记的位置。

#### 使用限制

- 可利用该参数显示多个定位点。
- 地点标注不支持设置英文。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| id | Number | 是 | 标记点 id，点击事件回调会返回此 id。 |
| latitude | Float | 是 | 纬度，范围 -90 ~ 90。 |
| longitude | Float | 是 | 经度，范围 -180 ~ 180。 |
| title | String | 否 | 标注点名。 |
| iconPath | String | 是 | 项目目录下的图片路径，不能用相对路径只能用 / 开头的绝对路径。<br />示例：/pages/image/test.jpg |
| iconLayout | Object | 否 | map 高级定制渲染绘制 marker 样式，优先级高于 iconPath, 对象参照 layout。<br /> src 支持：<ul><li>绝对路径：如 [https://gw.alipayobjects.com/XXX](https://gw.alipayobjects.com/XXX)。</li><li>相对路径（基准为项目根目录）：如 /marker/xiang.xml。</li></ul>**注意：** 相对路径不支持 ./marker/xiang.xml 方式。<br/> **版本要求：** 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| rotate | Number | 否 | 顺时针旋转的角度，范围 0 ~ 360，默认为 0。 |
| alpha | Number | 否 | 是否透明，默认为 1。 |
| width | Number | 否 | 默认为图片的实际宽度。 |
| height | Number | 否 | 默认为图片的实际高度。 |
| displayRanges | Array | 否 | 标明在特定地图缩放级别下展示。<br />[{<br />  "from": 10,<br />  "to": 15<br /> }]<br />**版本要求：** 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| callout | Object | 否 | 自定义 marker 上的气泡窗口，地图上最多同时展示一个，绑定 onCalloutTap。<br />{<br />    content:"xxx"<br />} |
| anchorX | Double | 否 | 经纬度在标注图标的锚点-横向值，这两个值需要成对出现，anchorX 表示横向(0-1)，Y 表示竖向(0-1)。<br />anchorX:0.5<br />anchorY:1 <br />表示底边中点。 |
| anchorY | Double | 否 |  |
| customCallout | Object | 否 | callout 背景自定义，目前只支持高德地图 style。<br />{<br />  "type": 2,<br />  "descList": [{<br />    "desc": "预计",<br />    "descColor": "#333333"<br />  }, {<br />    "desc": "5分钟",<br />    "descColor": "#108EE9"<br />  }, {<br />    "desc": "到达",<br />    "descColor": "#333333"<br />  }],<br />  "isShow": 1<br />} |
| iconAppendStr | String | 否 | 和 iconPath 一起使用，会将 iconPath 对应的图片及该字符串共同生成一个图片，当成 marker 的图标。 |
| iconAppendStrColor | String | 否 | 底部描述文本颜色。<br />**默认值**：#33B276。 |
| fixedPoint | Object | 否 | 基于屏幕位置扎点。<br />{<br />    //距离地图左上角的像素数,Number<br />    originX:100, <br />    originY:100  <br />} |
| markerLevel | Number | 否 | marker 在地图上的绘制层级，与地图上其他覆盖物统一的 Z 坐标系。<br />**版本要求：** 基础库 [1.0.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| label | Object | 否 | marker 上的气泡，地图上可同时展示多个，绑定 onMarkerTap。<br />{<br />    content:"Hello Label",<br />    color:"#000000",<br />    fontSize:12,<br />    borderRadius:"3",<br />    bgColor:"#ffffff",<br />    padding:5,<br />}<br />**版本要求：** 基础库 [1.12.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| style | Object | 否 | 自定义 marker 的样式和内容。<br />**版本要求：** 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
|  | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1536638990818-45f93fb6-f74f-4038-8302-b45fee25b7f1.png#width=435) |  |  |




### polygon
用于构造多边形对象。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| **points** | Array | 是 | 经纬度数组。<br />[{<br />  latitude: 0,<br />  longitude: 0<br />}]<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| color | String | 否 | 线的颜色，用 8 位十六进制表示，后两位表示 alpha 值，如：#eeeeeeAA。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| fillColor | String | 否 | 填充色，用 8 位十六进制表示，后两位表示 alpha 值，如：#eeeeeeAA。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| width | Number | 否 | 线的宽度。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| displayRanges | Array | 否 | 标明在特定地图缩放级别下展示。<br />[{<br />  "from": 12,<br />  "to": 17<br /> }]<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |


### polyline
用于指定一系列坐标点，从数组第一项连线至最后一项。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| points | Array | 是 | 经纬度数组。<br />[{<br />  latitude: 0,<br />  longitude: 0<br />}] |
| color | String | 否 | 线的颜色，用 8 位十六进制表示，后两位表示 alpha 值，如：#eeeeeeAA。 |
| width | Number | 否 | 线的宽度。 |
| dottedLine | Boolean | 否 | 是否虚线。<br />**默认值：** false |
| iconWidth | Number | 否 | 使用纹理时的宽度。<br />**版本要求：** 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| zIndex | Number | - | 覆盖物的 Z 轴坐标。<br />**版本要求：** 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| iconPath | String | - | 项目目录下的图片路径，可以用相对路径写法，以 '/' 开头则表示相对小程序根目录， 如果有 iconPath，会忽略 color。但是 `iconPath` 可以和 `colorList` 联合使用，这样纹理会浮在彩虹线上方，为避免覆盖彩虹线，纹理图片背景色可以设置透明。<br />**版本要求：** 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| colorList | Array | - | 彩虹线，分段依据 `points`。例如 `points` 有5个点，那么 `colorList` 就应该传 4 个颜色值，依此类推。如果 `colorList` 数量小于4，那么剩下的线路颜色和最后一个颜色一样。<br />[<br />  "#AAAAAA",<br />  "#BBBBBB"<br />]<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |


### circles
用于在地图上显示圆。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| latitude | Float | 是 | 纬度，范围 -90 ~ 90。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| longitude | Float | 是 | 经度，范围 -180 ~ 180。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| color | String | 否 | 描边的颜色，用 8 位十六进制表示，后两位表示 alpha 值，如：#eeeeeeAA。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| fillColor | String | 否 | 填充颜色，用 8 位十六进制表示，后两位表示 alpha 值，如：#eeeeeeAA。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| radius | Number | 是 | 半径（米）。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| strokeWidth | Number | 否 | 描边的宽度。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |


### controls
用于在地图上显示控件，控件不随着地图移动。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| id | Number | 否 | 控件 id，点击事件回调会返回此 id。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| position | Object | 是 | 控件在地图的位置。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| iconPath | String | 是 | 项目目录下的图片路径，可以用相对路径写法，以'/'开头则表示相对小程序根目录。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |
| clickable | Boolean | 否 | 是否可点击。<br />**默认值：** false。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 及以上 |


## position
控件在地图的位置，以及控件的大小。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| left | Number | 否 | 距离地图的左边界多远。<br />**默认值：** 0 |
| top | Number | 否 | 距离地图的上边界多远。<br />**默认值：** 0 |
| width | Number | 否 | 控件宽度。<br />**默认值：** 图片宽度 |
| height | Number | 否 | 控件高度。<br />**默认值：** 图片高度 |


## callout
自定义标记点上方的气泡窗口。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| content | String | 否 | 内容。<br />**默认值：** 为空（null） |


## customCallout
自定义 callout 背景。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| type | Number | 是 | 样式类型。0 为黑色 style，1 为白色 style，2 为背景+文本，见下图。<br />![](https://mdn.alipayobjects.com/afts/img/A*j18HQLU3tw4AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=TSUTe4_NdPFHIa6WeDzirAAAAABkMK8AAAAA#) |
| time | String | 是 | 时间值。 |
| descList | Array | 是 | 描述数组。<br />{ <br />    "type": 0,<br />    "time": "3",<br />    "descList": [{ <br />        "desc": "点击立即打车",<br />        "descColor": "#ffffff" <br />    }],<br />    "isShow": 1 <br />} |
| layout | Object | 否 | 使用 map 高级定制渲染。优先级最高, layout 对象参照 layout 定义。 |


### fixedPoint
基于屏幕位置的扎点。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| originX | Number | 是 | 横向像素点，距离地图左上角的像素数值，从 0 开始。 |
| originY | Number | 是 | 纵向像素点，距离地图左上角的像素数值，从 0 开始。 |

地图组件的经纬度是必须设置的, 若未设置经纬度，则默认是北京的经纬度。

## Marker 图鉴

### Marker 样式优先级说明

- customCallout，callout 与 label 互斥，优先级排序为：label > customCallout > callout 。
- style 与 icon 互斥，优先级排序为：style > iconAppendStr；style > icon。

### style
| **结构** | **图片示例** | **最低版本** |
| --- | --- | --- |
| {<br />    type:1,<br />    text1:"Style1",<br />    icon1:'xxx',<br />    icon2:'xxx'<br />} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537428922033-7f44ea7c-6f28-43cc-a5d0-80cc4cf0213b.png#width=200) | 1.11.0 |
| {<br />    type:2,<br />    text1:"Style2",<br />    icon1:'xxx',<br />    icon2:'xxx'<br />} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537428730637-bd21f41b-3352-4c42-a2ba-0dca4012b0e3.png#width=200) | 1.12.0 |
| {<br />    type:3,<br />    icon:xxx,  //选填<br />    text:xxx,  //必填<br />    color:xxx,  //默认#33B276<br />    bgColor:xxx,  //默认#FFFFFF  <br />    gravity:"left/center/right", //默认 center<br />    fontType:"small/standard/large"  //默认standard<br />} | ![](http://mdn.alipayobjects.com/afts/img/A*uTUwTr1D3m-bzN1EqNQH8gBkAa8wAA/original?bz=openpt_doc&t=jNguH-INECDw6xTVKqdWRwAAAABkMK8AAAAA#) | 1.13.0  |


### customCallout
| **结构** | **图片示例** | **最低版本** |
| --- | --- | --- |
| { <br />    "type": 0,<br />    "time": "3",<br />    "descList": [{ <br />        "desc": "点击立即打车",<br />        "descColor": "#ffffff" <br />    }],<br />    "isShow": 1 <br />} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537429397117-959401db-99f0-48b1-a15d-9817d441d978.png#width=200) | 1.10.0 |
| { <br />    "type": 1,<br />    "time": "3",<br />    "descList": [{ <br />        "desc": "点击立即打车",<br />        "descColor": "#333333" <br />    }],<br />    "isShow": 1 <br />} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537429638548-7a7dd421-7bc7-4849-8498-e8a9a3381618.png#width=208)<br />- | 1.10.0 |
| {<br />  "type": 2,<br />  "descList": [{<br />    "desc": "预计",<br />    "descColor": "#333333"<br />  }, {<br />    "desc": "5分钟",<br />    "descColor": "#108EE9"<br />  }, {<br />    "desc": "到达",<br />    "descColor": "#333333"<br />  }],<br />  "isShow": 1<br />} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537429958605-eff755af-bc25-40bd-b697-1d4c2e1be712.png#width=200) | 1.10.0 |


### label
| **属性** | **必填** | **默认值** |
| --- | --- | --- |
| content | 是 | - |
| color | 否 | 默认值："#000000" |
| fontsize | 否 | 默认值：14 |
| borderRadius | 否 | 默认值：20 |
| bgColor | 否 | 默认值："#FFFFFF" |
| padding | 否 | 默认值：10 |

| **结构** | **图鉴** | **最低版本** |
| --- | --- | --- |
| {<br />  content:"Hello Label",<br />  color:"#000000",<br />  fontSize:16,<br />  borderRadius:5,<br />  bgColor:"#ffffff",<br />  padding:12,<br />} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537430323991-11bf3fb8-58e7-4416-be4c-2700cdc8f3ec.png#width=200) | 10.1.38 |


## 错误码

- [Andriod 地图错误码对照表](https://lbs.amap.com/api/android-sdk/guide/map-tools/error-code)
- [iOS 地图错误码对照](https://lbs.amap.com/api/ios-sdk/guide/map-tool/errorcode/)

# FAQ

##  map 组件如何跳转到高德的 app 中去进行导航？
可使用 [my.openLocation](https://opendocs.alipay.com/mini/api/as9kin)。

##  map 组件 optimize 属性设置了 true 后如何获取 scale 值？
optimize 属性设置了 true 后，如果需要获取 scale 值，必须要使用 onRegionChange。

##  map组件是否支持海外功能？
目前不支持。

## 如何手动在地图上绘制多边形区域？
可以使用 polygon 进行绘制。

## iconAppendStr 里的文字能不能换行？
不支持。

## 地图组件里，设置了路径之后， 如何更改起点终点的 icon？
目前不支持更改。

# 相关文档

- [my.createMapContext](https://opendocs.alipay.com/mini/api/ui-map)
- [MapContext 概览](https://opendocs.alipay.com/mini/api/mapcontext)
- [点标记（Marker）图鉴](https://opendocs.alipay.com/mini/api/hpi21r)
- [map 高级定制渲染](https://opendocs.alipay.com/mini/00n21l)
