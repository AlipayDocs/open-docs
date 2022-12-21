# 简介

**MapContext.getMapProperties** 用于获取地图的属性信息。

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，支付宝客户端 10.1.82 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

```javascript
this.mapCtx = my.createMapContext('map');
this.mapCtx.getMapProperties({
  success: res => {
    console.log(res);
  },
});
```

## 返回值

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| is3d | Boolean | 是否是 3D 地图引擎。<br />更多信息可查看 [高德开放平台-3D 地图](https://lbs.amap.com/api/javascript-api/guide/map/3d-map/?sug_index=0)。<br /><br />版本限制：<ul><li>支付宝客户端 10.1.82 或更高版本。</li><li>基础库 1.23.0 或更高版本。</li></ul> |
| isSupportAnim | Boolean | 是否支持动画。<br /><br />版本限制：<ul><li>支付宝客户端 10.1.82 或更高版本。</li><li>基础库 1.23.0 或更高版本。</li></ul> |
| sdkName | String | 地图中使用的 SDK 名称。<br />更多信息可查看：<ul><li>[高德地图 Android SDK 简介](https://lbs.amap.com/api/android-sdk/summary/)</li><li>[高德地图 iOS SDK 简介](https://lbs.amap.com/api/ios-sdk/summary)</li></ul> 版本限制：<ul><li>支付宝客户端 10.1.90 或更高版本。</li><li>基础库 1.23.0 或更高版本。</li></ul> |
| sdkVersion | String | 地图中使用的 SDK 版本号。<br />更多信息可查看 ：<ul><li>[高德地图 Android SDK 简介](https://lbs.amap.com/api/android-sdk/summary/)</li><li>[高德地图 iOS SDK 简介](https://lbs.amap.com/api/ios-sdk/summary)</li></ul>版本限制：<ul><li>支付宝客户端 10.1.90 或更高版本。</li><li>基础库 1.23.0 或更高版本。</li></ul> |
| isSupportOversea | Boolean | 是否支持海外地图。<br /><br />版本限制：<ul><li>支付宝客户端 10.1.90 或更高版本。</li><li>基础库 1.23.0 或更高版本。</li></ul> |
| needStyleV7 | Boolean | 是否需要 7.x 版本自定义地图样式配置文件。<br />更多信息可查看 ：<ul><li>[高德地图 Android 自定义地图](https://lbs.amap.com/api/android-sdk/guide/create-map/custom/?sug_index=2)</li><li>[高德地图 iOS 自定义地图](https://lbs.amap.com/api/ios-sdk/guide/create-map/custom/?sug_index=1)</li></ul>版本限制：<ul><li>支付宝客户端 10.1.90 或更高版本。</li><li>基础库 1.23.0 或更高版本。</li></ul> |
