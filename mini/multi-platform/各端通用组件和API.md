每个端小程序所采用的框架和代码目录结构是一致的（点此查看 [小程序框架概述](https://opendocs.alipay.com/mini/framework/overview)）。另外基础组件和基础API 在各端也保持一致（在交互和视觉样式上需要对不同端进行适配）。

## 基础组件
| **分类** | **组件名称** |
| --- | --- |
| 视图容器 | [View](https://opendocs.alipay.com/mini/component/view) |
|  | [Swiper](https://opendocs.alipay.com/mini/component/swiper) |
|  | [Scroll View](https://opendocs.alipay.com/mini/component/scroll-view) |
| 基础内容 | [Text](https://opendocs.alipay.com/mini/component/text) |
|  | [Icon](https://opendocs.alipay.com/mini/component/icon) |
|  | [Progress](https://opendocs.alipay.com/mini/component/progress) |
| 表单组件 | [Button](https://opendocs.alipay.com/mini/component/button) |
|  | [Form](https://opendocs.alipay.com/mini/component/form) |
|  | [Label](https://opendocs.alipay.com/mini/component/label) |
|  | [Input](https://opendocs.alipay.com/mini/component/input) |
|  | [Textarea](https://opendocs.alipay.com/mini/component/textarea) |
|  | [Radio](https://opendocs.alipay.com/mini/component/radio) |
|  | [Checkbox](https://opendocs.alipay.com/mini/component/checkbox) |
|  | [Switch](https://opendocs.alipay.com/mini/component/switch) |
|  | [Slider](https://opendocs.alipay.com/mini/component/slider) |
|  | [Picker View](https://opendocs.alipay.com/mini/component/picker-view) |
|  | [Picker](https://opendocs.alipay.com/mini/component/picker) |
| 导航 | [Navigator](https://opendocs.alipay.com/mini/component/navigator) |
| 媒体组件 | [Image](https://opendocs.alipay.com/mini/component/image) |
| 画布 | [Canvas](https://opendocs.alipay.com/mini/component/canvas) |
| 地图 | [Map](https://opendocs.alipay.com/mini/component/map) |
| 开放组件 | [web-view](https://opendocs.alipay.com/mini/component/web-view) |


## 基础 API
| **分类** | **API 名称** |
| --- | --- |
| 网络 | [my.Request](https://opendocs.alipay.com/mini/api/owycmh) |
|  | [my.uploadFile](https://opendocs.alipay.com/mini/api/kmq4hc) |
|  | [my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r) |
| 开放接口 | [my.getAuthCode（用户授权/免登）](https://opendocs.alipay.com/mini/api/openapi-authorize) |
| 路由 | [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) |
|  | [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) |
|  | [my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) |
|  | [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) |
|  | [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) |
| 导航栏 | [my.setNavigationBar](https://opendocs.alipay.com/mini/api/xwq8e6) |
| 交互反馈 | [my.alert](https://opendocs.alipay.com/mini/api/ui-feedback) |
|  | [my.confirm](https://opendocs.alipay.com/mini/api/lt3uqc) |
|  | [my.showToast](https://opendocs.alipay.com/mini/api/fhur8f) |
|  | [my.showLoading](https://opendocs.alipay.com/mini/api/bm69kb) |
|  | [my.hideLoading](https://opendocs.alipay.com/mini/api/nzf540) |
|  | [my.showActionSheet](https://opendocs.alipay.com/mini/api/hr092g) |
| 下拉刷新 | [onPullDownRefresh](https://opendocs.alipay.com/mini/api/wo21qk) |
|  | [my.stopPullDownRefresh](https://opendocs.alipay.com/mini/api/pmhkbb) |
| 选择日期 | [my.datePicker](https://opendocs.alipay.com/mini/api/ui-date) |
| 动画 | [my.createAnimation](https://opendocs.alipay.com/mini/api/ui-animation) |
| 画布 | [my.createCanvasContext](https://opendocs.alipay.com/mini/api/ui-canvas) |
|  | [toTempFilePath](https://opendocs.alipay.com/mini/api/rod3ti) |
|  | [setTextAlign](https://opendocs.alipay.com/mini/api/rf1uma) |
|  | [setTextBaseline](https://opendocs.alipay.com/mini/api/wo3gqy) |
|  | [setFillStyle](https://opendocs.alipay.com/mini/api/vyfyp2) |
|  | [setStrokeStyle](https://opendocs.alipay.com/mini/api/lqmreg) |
|  | [setShadow](https://opendocs.alipay.com/mini/api/btvtra) |
|  | [createLinearGradient](https://opendocs.alipay.com/mini/api/qgb1mf) |
|  | [createCircularGradient](https://opendocs.alipay.com/mini/api/ix6opq) |
|  | [addColorStop](https://opendocs.alipay.com/mini/api/wtnm2p) |
|  | [setLineWidth](https://opendocs.alipay.com/mini/api/ugcrcq) |
|  | [setLineCap](https://opendocs.alipay.com/mini/api/de22sq) |
|  | [setLineJoin](https://opendocs.alipay.com/mini/api/sfqcgi) |
|  | [setMiterLimit](https://opendocs.alipay.com/mini/api/vul12s) |
|  | [rect](https://opendocs.alipay.com/mini/api/xgywt5) |
|  | [fillRect](https://opendocs.alipay.com/mini/api/vfpyra) |
|  | [strokeRect](https://opendocs.alipay.com/mini/api/vz04q8) |
|  | [clearRect](https://opendocs.alipay.com/mini/api/xg3h06) |
|  | [fill](https://opendocs.alipay.com/mini/api/yywmib) |
|  | [stroke](https://opendocs.alipay.com/mini/api/pgahxv) |
|  | [beginPath](https://opendocs.alipay.com/mini/api/vk0ohr) |
|  | [closePath](https://opendocs.alipay.com/mini/api/fg8c9b) |
|  | [moveTo](https://opendocs.alipay.com/mini/api/avy1f9) |
|  | [lineTo](https://opendocs.alipay.com/mini/api/zkno7s) |
|  | [arc](https://opendocs.alipay.com/mini/api/lut4uo) |
|  | [bezierCurveTo](https://opendocs.alipay.com/mini/api/dzf516) |
|  | [clip](https://opendocs.alipay.com/mini/api/rgl453) |
|  | [quadraticCurveTo](https://opendocs.alipay.com/mini/api/rq2yds) |
|  | [scale](https://opendocs.alipay.com/mini/api/gp3kpy) |
|  | [rotate](https://opendocs.alipay.com/mini/api/ncimzx) |
|  | [translate](https://opendocs.alipay.com/mini/api/lgqkb2) |
|  | [setFontSize](https://opendocs.alipay.com/mini/api/mg4uir) |
|  | [fillText](https://opendocs.alipay.com/mini/api/saf43s) |
|  | [drawImage](https://opendocs.alipay.com/mini/api/pzmtqk) |
|  | [setGlobalAlpha](https://opendocs.alipay.com/mini/api/cptvsl) |
|  | [save](https://opendocs.alipay.com/mini/api/qnyf7h) |
|  | [restore](https://opendocs.alipay.com/mini/api/gwoqt0) |
|  | [draw](https://opendocs.alipay.com/mini/api/he6iwx) |
| 键盘 | [my.hideKeyboard](https://opendocs.alipay.com/mini/api/ui-hidekeyboard) |
| 滚动 | [my.pageScrollTo](https://opendocs.alipay.com/mini/api/scroll) |
| 节点查询 | [my.createSelectorQuery](https://opendocs.alipay.com/mini/api/selector-query) |
|  | [SelectorQuery](https://opendocs.alipay.com/mini/api/pc8s51) |
|  | [selectorQuery.select](https://opendocs.alipay.com/mini/api/mwo97h) |
|  | [selectorQuery.selectAll](https://opendocs.alipay.com/mini/api/aygfvh) |
|  | [selectorQuery.selectViewport](https://opendocs.alipay.com/mini/api/kwbegi) |
|  | [selectorQuery.boundingClientRect](https://opendocs.alipay.com/mini/api/na4yun) |
|  | [selectorQuery.scrollOffset](https://opendocs.alipay.com/mini/api/euyxnr) |
|  | [selectorQuery.exec](https://opendocs.alipay.com/mini/api/baz2hg) |
| 分享 | [onShareAppMessage](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0) |
| 位置 | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) |
|  | [my.openLocation](https://opendocs.alipay.com/mini/api/as9kin) |
| 缓存 | [my.setStorage](https://opendocs.alipay.com/mini/api/eocm6v) |
|  | [my.setStorageSync](https://opendocs.alipay.com/mini/api/cog0du) |
|  | [my.getStorage](https://opendocs.alipay.com/mini/api/azfobl) |
|  | [my.getStorageSync](https://opendocs.alipay.com/mini/api/ox0wna) |
|  | [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) |
|  | [my.removeStorageSync](https://opendocs.alipay.com/mini/api/ytfrk4) |
| 多媒体 | 图片 |
|  | [my.chooseImage](https://opendocs.alipay.com/mini/006ld2) |
|  | [my.previewImage](https://opendocs.alipay.com/mini/006ldb) |
|  | [my.saveImage](https://opendocs.alipay.com/mini/006ldd) |
|  | [my.compressImage](https://opendocs.alipay.com/mini/006ld5) |
|  | [my.getImageInfo](https://opendocs.alipay.com/mini/006ld9) |
| 设备 | 系统信息 |
|  | [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use) |
|  | [my.getSystemInfo](https://opendocs.alipay.com/mini/api/system-info) |
|  | [my.getSystemInfoSync](https://opendocs.alipay.com/mini/api/gawhvz) |
|  | 网络状态 |
|  | [my.getNetworkType](https://opendocs.alipay.com/mini/api/network-status) |
|  | 剪贴板 |
|  | [my.setClipboard](https://opendocs.alipay.com/mini/api/klbkbp) |
|  | [my.getClipboard](https://opendocs.alipay.com/mini/api/clipboard) |
|  | 振动 |
|  | [my.vibrate](https://opendocs.alipay.com/mini/api/vibrate) |
| 蓝牙（钉钉端未支持） | [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4) |
|  | [my.closeBluetoothAdapter](https://opendocs.alipay.com/mini/api/wvko0w) |
|  | [my.getBluetoothAdapterState](https://opendocs.alipay.com/mini/api/eid4o6) |
|  | [my.startBluetoothDevicesDiscovery](https://opendocs.alipay.com/mini/api/ksew43) |
|  | [my.stopBluetoothDevicesDiscovery](https://opendocs.alipay.com/mini/api/syb4mi) |
|  | [my.getBluetoothDevices](https://opendocs.alipay.com/mini/api/pelizr) |
|  | [my.getConnectedBluetoothDevices](https://opendocs.alipay.com/mini/api/ge8nue) |
|  | [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) |
|  | [my.disconnectBLEDevice](https://opendocs.alipay.com/mini/api/yqrmmk) |
|  | [my.writeBLECharacteristicValue](https://opendocs.alipay.com/mini/api/vmp2r4) |
|  | [my.readBLECharacteristicValue](https://opendocs.alipay.com/mini/api/zro0ka) |
|  | [my.notifyBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/pdzk44) |
|  | [my.getBLEDeviceServices](https://opendocs.alipay.com/mini/api/uzsg75) |
|  | [my.getBLEDeviceCharacteristics](https://opendocs.alipay.com/mini/api/fmg9gg) |
|  | [my.onBluetoothDeviceFound](https://opendocs.alipay.com/mini/api/mhzls9) |
|  | [my.offBluetoothDeviceFound](https://opendocs.alipay.com/mini/api/snw2t7) |
|  | [my.onBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/cdu501) |
|  | [my.offBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/dlxobk) |
|  | [my.onBLEConnectionStateChanged](https://opendocs.alipay.com/mini/api/utgyiu) |
|  | [my.offBLEConnectionStateChanged](https://opendocs.alipay.com/mini/api/xfuy7k) |
|  | [my.onBluetoothAdapterStateChange](https://opendocs.alipay.com/mini/api/eegfbk) |
|  | [my.offBluetoothAdapterStateChange](https://opendocs.alipay.com/mini/api/ocgwfe) |
| iBeacon（钉钉端未支持） | [my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k) |
|  | [my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) |
|  | [my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc) |
|  | [my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y) |
|  | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7) |
| 扫码 | [my.scan](https://opendocs.alipay.com/mini/api/scan) |

