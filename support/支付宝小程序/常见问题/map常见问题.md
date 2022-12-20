# 前提条件
- 支持高德地图 style 与火星坐标系。
- 支持通过同层渲染实现 [cover-view](https://opendocs.alipay.com/mini/component/cover-view) 覆盖 map 组件。同层渲染支持范围 10.1.35 及其以上版本 Android 的小程序，10.1.50 及其以上版本 iOS 的小程序。
- 不支持在 [scroll-view](https://opendocs.alipay.com/mini/component/scroll-view) 中使用 map 组件。
- 不支持使用 CSS 动画，CSS 动画对 map 组件无效。
- 不支持小程序获取当前地图的经纬度。
- 缩小或者放大了地图比例尺之后，若再次设置 data 经纬度到一个地点，请在 onRegionChange 函数中重新设置 data 的 scale 值，否则会出现拖动地图区域后，重新加载导致地图比例尺又变回缩放前的大小，具体请参照示例代码 regionchange 函数部分。
- 基础库 1.18.5 开始支持 optimize 属性，开启 optimize 后，开发者不需要再监听 onRegionChange 来更新 scale 属性值以保证缩放比例不变。此特性在客户端 10.1.68 以上支持，可通过 [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use)（map.optimize）进行检测。 

# 常见问题

### 地图组件铺满全屏
问题场景：用系统信息算出屏幕高度后赋值给地图组件和一个底部的控制组件，会有一个间隙。<br />问题原因：css的样式排版问题，由于地图有时候不会自动铺满这个高度会导致留下一段底边。<br />解决方案：在外部嵌套一层，并设置 map100% 占据这个高度即可。 

### 地图中可以使用swiper组件吗
[swiper](https://opendocs.alipay.com/mini/component/swiper) 组件目前不支持在地图中使用。 

### 小程序里打开地图APP
目前无法直接从小程序唤起打开地图APP，可以通过 [my.openLocation](https://opendocs.alipay.com/mini/api/as9kin) 打开内置地图然后导航打开高德地图APP。 

### map高级定制渲染不显示
参考[map高级定制渲染不显示](https://opendocs.alipay.com/support/01rb77)。 

### 取消显示指南针无效
调用 this.mapCtx.showsScale({isShowsScale:0}); 取消显示指南针，但无效果。<br />由于 onLoad 时 map 在初始化，并未渲染完成，onLoad 中调用 this.mapCtx.showsScale 会导致不生效，建议放在 onReady 中调用。 

### 地图中controls定位在右下
实现地图右下角 controls 定位需要自己进行计算来定位，也是使用 left 和 top。<br />假设：地图的宽高分别为300:600，controls 的宽高为50:50，那么实现右下就是 position为left：300-50 ，top：600-50。 

### 如何实现在map上添加一个图标
可以使用 [cover-image](https://opendocs.alipay.com/mini/component/cover-image) 来实现 map 之上显示图片的效果，使用 cover-view 在 map 之上显示文字的效果。
```html
<view class="page-section-demo" 
      style="position: relative;"> 
  <map id="map" longitude="120.131441" latitude="30.279383"    
       show-location style="width: 400px; height: 300px;"  
       />  
  <cover-view onTap="onCoverViewTap"   
              style="text-align: center;
                     width: 100px; 
                     height: px;
                     position: absolute;
                     left: 20px; top: 10px;
                     color:white;
                     font-size: 20px;
                     background-color: rgba(0, 0, 255, 0.5)">1111</cover-view> 
  <cover-image onTap="onCoverImageTap" 
               style="height: 50px;width: 50px;position: absolute; top: 100px;left: 10px;"     
               src="/pages/storeTest/11111.webp"/><!--图片地址换成需自己的项目地址-->
</view>
```
 

### 小程序是否可以调用高德地图API
小程序可以调用高德地图的方法，但是需要在后台管理里添加请求域名白名单。详情可查看 [高德](https://lbs.amap.com/api/webservice/summary) 。

### 小程序的地图组件默认支持海外地图么
目前不支持。

### map组件optimize属性设置true后 ，如何获取scale的值
map 地图组件中 optimize 属性设置 true 后，仍需要使用 onRegionChange 方法去获取 scale 值。 

## markers

### iconPath用绝对路径
地图组件 marker 中 iconPath 项目目录下的图片路径，不能用相对路径只能用 / 开头的绝对路径。<br />示例：`/pages/image/test.jpg`。 

### Marker样式优先级说明
customcallout，callout 和 label 互斥，优先级：label > customcallout > callout。<br />style 与 icon 互斥，优先级：style > iconAppendStr；style > icon 。

### map组件里markers不显示的原因

- markers 的 iconPath 传入的路径不对，导致图标不显示。
- markers 的经纬度不对，值不规范或者超出地图当前的视野范围。
- 宽高设置过小，或者透明度太高。 

### 地图上的label标签加了边框线不显示
不支持添加边框，目前只支持参数：

- content：必填
- color：选填，默认"#000000"
- fontsize：选填，默认14
- borderRadius：选填，默认20
- bgColor：选填，默认"#FFFFFF"
- padding：选填，默认10 

### 一个marker是否可以设置多个label
一个 marker 只能设置一个 label；需要在地图中显示多个 label，可以设置多个 marker 实现。 

### markers更新后地图中心位置改变
更新 markers 的时候使用 setdata 导致地图重新加载，从而导致这个问题。在更新 markers 的时候，同时更新 map 的中心点。 

## MapContext

### 小程序地图导航
可以使用地图的 [MapContext.showRoute(Object)](https://opendocs.alipay.com/mini/api/uwffxx) 接口实现导航，导航路线需自行实现，默认规划步行路线，只能显示一条。详细参考 [my.createMapContext](https://opendocs.alipay.com/mini/api/ui-map) 文档。 

### 地图规划步行路线自定纹理不显示
[MapContext.showRoute](https://opendocs.alipay.com/mini/api/uwffxx) 的 iconPath 需要的图片大小有所要求：

- 基础库 1.11.0 及以下版本中，3D 地图中该参数优先级高于 routeColor，即纹理会覆盖颜色值。
- 基础库 1.13.0 及以上版本建议不设置该参数，因为在 3D 地图下提供了默认的纹理图案，图片尺寸建议为 2 的整数幂，如64*64。 

### mapCtx.showRoute收不到回调success
IDE 模拟器暂无法获得返回值，需真机预览获得返回值。 

### MapContext.translateMarker(Object)方法在iOS上不能移动marker
在 iOS 上需要添加上 animationEnd()方法，才能正常执行。<br />示例代码：
```javascript
this.mapCtx.translateMarker({      
  markerId:xxx, // 必填  
  destination:{ 
    longitude:xxx,latitude:xxx // 必填       
  },        
  autoRotate:true/false, // 选填，默认true   
  rotate:xxx, // 选填，在autoRotate为false的情况下才有效，不填默认是0    
  duration:100, // 选填，单位ms，默认1000ms     
  animationEnd:xxx //function 动画结束回调});
```

