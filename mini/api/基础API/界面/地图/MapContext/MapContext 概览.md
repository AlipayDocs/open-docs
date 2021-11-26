MapContext 实例，可通过 [my.createMapContext ](https://opendocs.alipay.com/mini/api/ui-map)获取。

MapContext 通过 ID 跟一个 map 组件绑定，操作对应的 [map 组件](https://opendocs.alipay.com/mini/component/map)。

## 方法列表

| **名称** | **说明** |
| --- | --- |
| [MapContext.calculateDistance](https://opendocs.alipay.com/mini/00nfnc) | 地图路径计算能力，用于计算途径地图上多个点的总路线距离。也可根据该路线截取部分子路线，加上其他目标点的路径规划后，组合成新的路径。 |
| [MapContext.changeMarkers](https://opendocs.alipay.com/mini/00k9uj) | 添加、删除、更新指定的标记（marker）。 |
| [MapContext.clearRoute](https://opendocs.alipay.com/mini/api/qb6sf9) | 清除地图上的步行导航路线。 |
| [MapContext.gestureEnable](https://opendocs.alipay.com/mini/api/sgwf36) | 设置所有手势是否可用。 |
| [MapContext.getCurrentLocation](https://opendocs.alipay.com/mini/api/vc2gdt) | 获取当前地图中心位置。 |
| [MapContext.getMapProperties](https://opendocs.alipay.com/mini/00nfn7) | 获取地图的属性信息。 |
| [MapContext.getRegion](https://opendocs.alipay.com/mini/00nbqs) | 获取地图东北角、西南角的经纬度，从而获取地图整体的视野范围。 |
| [MapContext.getRotate](https://opendocs.alipay.com/mini/api/getrotate) | 获取当前地图的旋转角。 |
| [MapContext.getScale](https://opendocs.alipay.com/mini/api/getScale) | 获取地图的缩放级别。 |
| [MapContext.getSkew](https://opendocs.alipay.com/mini/api/getskew) | 获取当前地图的倾斜角。 |
| [MapContext.includePoints](https://opendocs.alipay.com/mini/api/includepoints) | 缩放视野到指定可视区域。 |
| [MapContext.mapToScreen](https://opendocs.alipay.com/mini/api/mapToScreen) | 将地图经纬度坐标系转换成屏幕坐标系。 |
| [MapContext.moveToLocation](https://opendocs.alipay.com/mini/api/ans8wt) | 移动视野到定位点并恢复到默认缩放级别，需要配合 map 组件的 show-location 使用。 |
| [MapContext.polygonContainsPoint](https://opendocs.alipay.com/mini/api/polygonContainsPoint) | 判断矩形区域是否包含传入的经纬度点。 |
| [MapContext.screenToMap](https://opendocs.alipay.com/mini/api/screenToMap) | 将屏幕坐标系转换成地图经纬度坐标系。 |
| [MapContext.setCenterOffset](https://opendocs.alipay.com/mini/api/setcenteroffset) | 设置地图中心点偏移。 |
| [MapContext.setMapType](https://opendocs.alipay.com/mini/api/setmaptype) | 设置地图主题类型。 |
| [MapContext.showRoute](https://opendocs.alipay.com/mini/api/uwffxx) | 默认规划步行路线，只能显示一条。 |
| [MapContext.showsCompass](https://opendocs.alipay.com/mini/api/rcsrn9) | 设置指南针是否可见。 |
| [MapContext.showsScale](https://opendocs.alipay.com/mini/api/gxk4r0) | 设置比例尺控件是否可见。 |
| [MapContext.smoothMoveMarker](https://opendocs.alipay.com/mini/00nedv) | 指定标记（marker）进行动画。 |
| [MapContext.smoothMovePolyline](https://opendocs.alipay.com/mini/00nd0e) | 轨迹动画。 |
| [MapContext.translateMarker](https://opendocs.alipay.com/mini/api/sg7chr) | 平移 marker 接口。 |
| [MapContext.updateComponents](https://opendocs.alipay.com/mini/api/bph944) | 增量更新地图接口。 |


## 错误码
错误码信息请参见：

- [Andriod 地图错误码对照表](https://lbs.amap.com/api/android-sdk/guide/map-tools/error-code)
- [iOS 地图错误码对照](https://lbs.amap.com/api/ios-sdk/guide/map-tool/errorcode/)



