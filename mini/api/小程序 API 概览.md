
# 简介
本文归纳了支付宝小程序前端 API 及其作用。<br />

**说明：**

- 前端接口使用说明参见 [小程序 API 使用说明](https://opendocs.alipay.com/mini/api/overview)。
- 错误码信息请参见 [小程序 API 错误码对照表](https://opendocs.alipay.com/mini/00nmrr)。<br />

# 基础
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use) | 判断当前小程序的 API、入参或返回值、组件、属性等在当前版本是否支持。 | ✓ | ✓ |
| [my.env](https://opendocs.alipay.com/mini/api/env) | 小程序环境变量对象 API。 | ✓ | ✓ |
| [my.base64ToArrayBuffer](https://opendocs.alipay.com/mini/api/021zmy) | 将 Base64 字符串转成 ArrayBuffer 对象。 | ✓ | ✓ |
| [my.arrayBufferToBase64](https://opendocs.alipay.com/mini/api/021zmz) | 将 ArrayBuffer 对象转成 Base64 字符串。 | ✓ | ✓ |
| [my.getAppIdSync](https://opendocs.alipay.com/mini/api/gazkkm) | 同步获取小程序 APPID。 | ✓ | ✓ |
| [my.getLaunchOptionsSync](https://opendocs.alipay.com/mini/api/getLaunchOptionsSync) | 获取小程序启动时的参数。 | ✓ | ✓ |
| [my.getRunScene](https://opendocs.alipay.com/mini/api/runscene) | 获取当前小程序的运行版本。 | ✓ | ✓ |
| [my.SDKVersion](https://opendocs.alipay.com/mini/api/sdk-version) | 获取基础库版本号。 | ✓ | ✓ |
| [my.getEnterOptionsSync](https://opendocs.alipay.com/mini/api/029i75) | 获取本次小程序启动时的参数。 | ✓ | ✓ |


# 应用级事件
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.onAppHide](https://opendocs.alipay.com/mini/api/tv6qvi) | 监听小程序切后台事件。 | ✓ | ✓ |
| [my.offAppHide](https://opendocs.alipay.com/mini/api/dldh0a) | 取消监听小程序切后台事件。 | ✓ | ✓ |
| [my.onAppShow](https://opendocs.alipay.com/mini/api/nn7do1) | 监听小程序切前台事件。 | ✓ | ✓ |
| [my.offAppShow](https://opendocs.alipay.com/mini/api/tkohmw) | 取消监听小程序切前台事件。 | ✓ | ✓ |
| [my.onComponentError](https://opendocs.alipay.com/mini/api/oncomponent) | 监听小程序自定义组件内部 JS 代码的 error 事件 | ✓ | ✓ |
| [my.offComponentError](https://opendocs.alipay.com/mini/api/offcomponent) | 取消监听小程序自定义组件内部 JS 代码的 error 事件。 | ✓ | ✓ |
| [my.onError](https://opendocs.alipay.com/mini/00nnsx) | 监听小程序错误事件。 | ✓ | ✓ |
| [my.offError](https://opendocs.alipay.com/mini/00njqm) | 取消监听小程序错误事件。 | ✓ | ✓ |
| [my.onPageNotFound](https://opendocs.alipay.com/mini/01zdng) | 监听小程序要打开的页面不存在事件。 | ✓ | ✓ |
| [my.offPageNotFound](https://opendocs.alipay.com/mini/01zarw) | 取消监听小程序要打开的页面不存在事件。 | ✓ | ✓ |
| [my.onUnhandledRejection](https://opendocs.alipay.com/mini/00nd0f) | 监听未处理的 Promise 拒绝事件（即 unhandledrejection 事件）。 | ✓ | ✓ |
| [my.offUnhandledRejection](https://opendocs.alipay.com/mini/00nfnd) | 取消监听 unhandledrejection 事件。 | ✓ | ✓ |


# 界面

## 导航栏
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getTitleColor](https://opendocs.alipay.com/mini/api/dplf2s) | 获取导航栏背景色。 | ✓ | ✓ |
| [my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) | 隐藏 TitleBar 上的返回首页图标，和通用菜单中的返回首页功能。 | ✓ | ✓ |
| [my.hideNavigationBarLoading](https://opendocs.alipay.com/mini/api/ncgsga) | 在当前页面隐藏导航条加载动画。 | ✓ | ✓ |
| [my.setNavigationBar](https://opendocs.alipay.com/mini/api/xwq8e6) | 设置导航栏文字及样式。 | ✓ | ✓ |
| [my.showNavigationBarLoading](https://opendocs.alipay.com/mini/api/lydg2a) | 在当前页面显示导航条加载动画。 | ✓ | ✓ |
| [导航栏 FAQ](https://opendocs.alipay.com/mini/007l6m) | 对导航栏的常见问题解答。 | - | - |


## TabBar
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.hideTabBar](https://opendocs.alipay.com/mini/api/at18z8) | 隐藏 TabBar。 | ✓ | ✓ |
| [my.hideTabBarRedDot](https://opendocs.alipay.com/mini/api/mg428a) | 隐藏 TabBar 某一项的右上角的红点。 | ✓ | ✓ |
| [my.removeTabBarBadge](https://opendocs.alipay.com/mini/api/lpbp5g) | 移除 TabBar 某一项右上角的文本。 | ✓ | ✓ |
| [my.setTabBarBadge](https://opendocs.alipay.com/mini/api/qm7t3v) | 为 TabBar 某一项的右上角添加文本。 | ✓ | ✓ |
| [my.setTabBarItem](https://opendocs.alipay.com/mini/api/zu37bk) | 动态设置 TabBar 某一项的内容。 | ✓ | ✓ |
| [my.setTabBarStyle](https://opendocs.alipay.com/mini/api/wcf0sv) | 动态设置 TabBar 的整体样式。 | ✓ | ✓ |
| [my.showTabBar](https://opendocs.alipay.com/mini/api/dpq5dh) | 显示 TabBar。 | ✓ | ✓ |
| [my.showTabBarRedDot](api/dquxiq) | 显示 TabBar 某一项的右上角的红点。 | ✓ | ✓ |
| [onTabItemTap](api/navg36) | 点击 Tab 时触发。 | ✓ | ✓ |
| [TabBar 常见问题](/mini/api/do7urq) | 对 TabBar 标签的常见问题解答。 | - | - |


## 路由
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.switchTab](api/ui-tabbar) | 跳转到指定 TabBar 页面，并关闭其他所有非 TabBar 页面。 | ✓ | ✓ |
| [my.reLaunch](api/hmn54z) | 关闭当前所有页面，跳转到应用内的某个指定页面。 | ✓ | ✓ |
| [my.redirectTo](api/fh18ky) | 关闭当前页面，跳转到应用内的某个指定页面。 | ✓ | ✓ |
| [my.navigateTo](api/zwi8gx) | 从当前页面，跳转到应用内的某个指定页面，可以使用 [my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) 返回到原来页面。 | ✓ | ✓ |
| [EventChannel](https://opendocs.alipay.com/mini/api/eventchannel) | 页面间事件通信通道。 | ✓ | ✓ |
| [my.navigateBack](api/kc5zbx) | 关闭当前页面，返回上一级或多级页面。 | ✓ | ✓ |
| [路由 FAQ](/mini/api/fu8l65) | 对路由的常见问题解答。 | - | - |


## 交互反馈
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.alert](api/ui-feedback) | 警告框。 | ✓ | ✓ |
| [my.confirm](api/lt3uqc) | 确认框。 | ✓ | ✓ |
| [my.prompt](api/vqpy01) | 弹出一个对话框，让用户在对话框内输入文本。 | ✓ | ✓ |
| [my.showToast](api/fhur8f) | 显示一个弱提示，可选择多少秒之后消失。 | ✓ | ✓ |
| [my.hideLoading](api/nzf540) | 隐藏加载提示。 | ✓ | ✓ |
| [my.hideToast](/mini/api/iygd4e) | 隐藏弱提示。 | ✓ | ✓ |
| [my.showLoading](/mini/api/bm69kb) | 显示加载提示。 | ✓ | ✓ |
| [my.showActionSheet](api/hr092g) | 显示操作菜单。 | ✓ | ✓ |


## 下拉刷新
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [onPullDownRefresh](api/wo21qk) | 监听该页面用户的下拉刷新事件。 | ✓ | ✓ |
| [my.stopPullDownRefresh](api/pmhkbb) | 停止当前页面的下拉刷新。 | ✓ | ✓ |
| [my.startPullDownRefresh](api/ui-pulldown) | 开始下拉刷新。 | ✓ | ✓ |


## 联系人
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.choosePhoneContact](api/blghgl) | 选择本地系统通信录中某个联系人的电话。 | ✓ | ✓ |
| [my.chooseAlipayContact](api/ui-contact) | 唤起支付宝通讯录，选择一个或者多个支付宝联系人。 | ✓ | ✓ |
| [my.chooseContact](api/eqx2u5) | 唤起选择联系人组件。 | ✓ | ✓ |


## 选择城市
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.chooseCity](api/ui-city) | 打开城市选择列表。 | ✓ | ✓ |
| [my.offLocatedComplete](https://opendocs.alipay.com/mini/api/offLocatedComplete) | 取消监听地理位置定位完成事件。 | ✗ | ✓ |
| [my.onLocatedComplete](/mini/api/krzyo1) | 监听地理位置定位完成事件。 | ✗ | ✓ |
| [my.setLocatedCity](/mini/api/yw382g) | 修改 [my.chooseCity](/mini/api/ui-city) 中的默认定位城市的名称。 | ✗ | ✓ |
| [my.regionPicker](https://opendocs.alipay.com/mini/00nd0d) | 多级省市区选择器，自带省市区数据源。 | ✗ | ✓ |


## 选择地区
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.chooseDistrict](https://opendocs.alipay.com/mini/api/choosedistrict) | 使用支付宝统一样式选择地区。 | ✗ | ✓ |


## 选择日期
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.datePicker](api/ui-date) | 打开日期选择列表。 | ✓ | ✓ |


## 动画
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createAnimation](api/ui-animation) | 创建动画实例。 | ✓ | ✓ |


## 画布
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createOffscreenCanvas](https://opendocs.alipay.com/mini/api/021zn0) | 创建离屏 canvas 实例。 | ✓ | ✓ |
| [my.createCanvasContext](https://opendocs.alipay.com/mini/api/ui-canvas) | 创建 canvas 绘图上下文。 | ✓ | ✓ |
| [RenderingContext](https://opendocs.alipay.com/mini/01w0it) | Canvas 绘图上下文 | ✓ | ✓ |
| [Canvas](https://opendocs.alipay.com/mini/01vzqv) | Canvas 实例。 | ✓ | ✓ |
| [Image](https://opendocs.alipay.com/mini/01vyku) | 图片对象，当调用 [Canvas.createImage](https://opendocs.alipay.com/mini/api/createimage) 方法时返回此对象。 | ✓ | ✓ |


## 地图
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createMapContext](api/ui-map) | 创建并返回一个 map 上下文对象 [mapContext](https://opendocs.alipay.com/mini/api/mapcontext)。 | ✓ | ✓ |
| [my.getMapInfo](https://opendocs.alipay.com/mini/api/getmapinfo) | 获取地图基础信息。 | ✗ | ✓ |


## 计算路径
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.calculateRoute](/mini/api/calculate-route) | 计算路径 API。根据起点和终点的地理位置，智能规划最佳出行路线，并计算不同出行方式下的行动距离和所需时间，默认规划步行路线，支持规划步行、公交、骑行和驾车四种路线。 | ✗ | ✓ |


## 键盘
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.hideKeyboard](api/ui-hidekeyboard) | 隐藏键盘。 | ✓ | ✓ |


## 滚动
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.pageScrollTo](api/scroll) | 滚动到页面的目标位置。 | ✓ | ✓ |


## 节点查询
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createIntersectionObserver](api/intersectionobserver) | 创建并返回一个 IntersectionObserver 对象实例。 | ✓ | ✓ |
| [my.createSelectorQuery](api/selector-query) | 获取一个节点查询对象 SelectorQuery。 | ✓ | ✓ |


## 选项选择器
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.optionsSelect](api/options-select) | 类似于 safari 原生 select 的组件，但是功能更加强大，一般用来替代 select，或者 2 级数据的选择。注意不支持 2 级数据之间的联动。 | ✓ | ✓ |


## 级联选择
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.multiLevelSelect](/mini/api/multi-level-select) | 级联选择功能，主要使用在于多级关联数据选择。 | ✓ | ✓ |


## 设置窗口背景
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.setBackgroundColor](api/set-background) | 动态设置窗口的背景色。 | ✓ | ✓ |
| [my.setBackgroundTextStyle](api/aamqae) | 动态设置下拉背景字体、loading 图的样式。 | ✗ | ✓ |


## 设置页面是否支持下拉
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.setCanPullDown](/mini/api/set-can-pull-down) | 设置页面是否支持下拉。 | ✓ | ✓ |


## 字体
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.loadFontFace](api/ggawf0) | 动态加载网络字体。 | ✓ | ✓ |


# 多媒体

## 图片
| 名称 | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage) | 拍照或从手机相册中选择图片。 | ✓ | ✓ |
| [my.compressImage](https://opendocs.alipay.com/mini/api/media/image/my.compressimage) | 压缩图片。 | ✓ | ✓ |
| [my.getImageInfo](https://opendocs.alipay.com/mini/api/media/image/my.getimageinfo) | 获取图片信息。 | ✓ | ✓ |
| [my.generateImageFromCode](https://opendocs.alipay.com/mini/api/media/image/my.generateimagefromcode) | 生成二维码，由客户端生成，速度快且不耗流量。 | ✓ | ✓ |
| [my.previewImage](https://opendocs.alipay.com/mini/api/media/image/my.previewimage) | 预览图片。 | ✓ | ✓ |
| [my.saveImage](https://opendocs.alipay.com/mini/api/media/image/my.saveimage) | 保存在线图片到手机相册。 | ✓ | ✓ |
| [my.saveImageToPhotosAlbum](https://opendocs.alipay.com/mini/api/media/image/my.saveImagetophotosalbum) | 保存图片到系统相册。 | ✗ | ✓ |


## 视频
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 小程序里内嵌入视频组件，即可上传并播放视频。 my.createVideoContext 用于创建并返回一个 videoId 上下文对象 videoContext。 | ✗ | ✓ |
| [my.chooseVideo](https://opendocs.alipay.com/mini/api/media/video/my.choosevideo) | 拍摄视频或从手机相册中选视频。 | ✓ | ✓ |
| [my.saveVideoToPhotosAlbum](https://opendocs.alipay.com/mini/api/media/video/my.savevideotophotosalbum) | 保存视频到相册。 | ✗ | ✓ |


## 音频播放
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createInnerAudioContext](https://opendocs.alipay.com/mini/00bg4q) | 在小程序内创建并返回内部音频（与背景音频相对应） innerAudioContext 对象。又称“前景音频”。 | ✓ | ✓ |
| [my.getAvailableAudioSources](https://opendocs.alipay.com/mini/00bg4t) | 获取当前支持的音频输入源。 | ✓ | ✓ |
| [my.getBackgroundAudioManager](https://opendocs.alipay.com/mini/00bifu) | 获取后台音频播放器，与前景音频相对应，可以在用户离开当前小程序后继续播放音频。 | ✓ | ✓ |
| [my.offAudioInterruptionBegin](https://opendocs.alipay.com/mini/00jim9) | 取消监听音频因为系统占用而被中断的开始事件。 | ✓ | ✓ |
| [my.offAudioInterruptionEnd](https://opendocs.alipay.com/mini/00jfja) | 取消监听音频被中断的结束事件。 | ✓ | ✓ |
| [my.onAudioInterruptionBegin](https://opendocs.alipay.com/mini/00jim8) | 监听音频因为系统占用而被中断的开始事件。 | ✓ | ✓ |
| [my.onAudioInterruptionEnd](https://opendocs.alipay.com/mini/00jgot) | 监听音频被中断的结束事件。 | ✓ | ✓ |


## 录音
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getRecorderManager](https://opendocs.alipay.com/mini/api/getrecordermanager) | 获取全局唯一的录音管理器 RecorderManager。 | ✗ | ✓ |


## lottie 动画
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createLottieContext](https://opendocs.alipay.com/mini/api/createlottiecontext) | Lottie 是一个用于 Web 和 iOS 的移动库，可使用 Bodymovin 解析以 JSON 格式导出的 Adobe After Effects 动画，并将其本地呈现在移动设备上。<br />my.createLottieContext 用于创建并返回一个 lottieId 上下文对象 lottieContext。 | ✓ | ✓ |


# 缓存
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [缓存 API 概览](https://opendocs.alipay.com/mini/api/qm3ggk) | 介绍 API 的操作、描述等信息。 | ✓ | ✓ |
| [my.setStorage](api/eocm6v) | 将数据存储在本地缓存中指定的 key 中的异步接口。 | ✓ | ✓ |
| [my.setStorageSync](api/cog0du) | 同步将数据存储在本地缓存中指定的 key 中的同步接口。 | ✓ | ✓ |
| [my.getStorage](api/azfobl) | 获取缓存数据的异步接口。 | ✓ | ✓ |
| [my.getStorageSync](api/ox0wna) | 获取缓存数据的同步接口。 | ✓ | ✓ |
| [my.removeStorage](api/of9hze) | 删除缓存数据的异步接口。 | ✓ | ✓ |
| [my.removeStorageSync](api/ytfrk4) | 删除缓存数据的同步接口。 | ✓ | ✓ |
| [my.clearStorage](api/storage) | 清除本地数据缓存的异步接口。 | ✓ | ✓ |
| [my.clearStorageSync](api/ulv85u) | 清除本地数据缓存的同步接口。 | ✓ | ✓ |
| [my.getStorageInfo](/mini/api/zvmanq) | 获取当前 storage 的相关信息的异步接口。 | ✓ | ✓ |
| [my.getStorageInfoSync](api/uw5rdl) | 获取当前 storage 相关信息的同步接口。 | ✓ | ✓ |


# 文件
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getFileSystemManager](https://opendocs.alipay.com/mini/api/0226oc) | 获取全局唯一的文件管理器。 | ✓ | ✓ |
| [my.getFileInfo](api/file) | 获取文件信息。 | ✓ | ✓ |
| [my.getSavedFileInfo](api/qrx6ze) | 获取保存的文件信息。 | ✓ | ✓ |
| [my.getSavedFileList](api/cgohg1) | 获取保存的所有文件信息。 | ✓ | ✓ |
| [my.openDocument](/mini/api/mwpprc) | 在新页面打开文件预览，暂时只支持预览 PDF 格式文件。 | ✓ | ✓ |
| [my.removeSavedFile](api/dgi1fr) | 删除某个保存的文件。 | ✓ | ✓ |
| [my.saveFile](api/xbll1q) | 保存文件到本地。 | ✓ | ✓ |
| [Stats](https://opendocs.alipay.com/mini/api/stats) | 描述文件状态的对象。 | ✓ | ✓ |


# 位置
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getLocation](api/mkxuqd) | 获取用户当前的地理位置信息。 | ✓ | ✓ |
| [my.openLocation](api/as9kin) | 使用支付宝内置地图查看位置。 | ✓ | ✓ |
| [my.chooseLocation](api/location) | 使用支付宝内置地图选择地理位置。 | ✓ | ✓ |


# 网络
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.request](api/owycmh) | 小程序网络请求。 | ✓ | ✓ |
| [my.request 常见问题](https://opendocs.alipay.com/mini/00hxw8) | 对 my.request 的常见问题解答。 | - | - |
| [my.uploadFile](api/kmq4hc) | 上传本地资源到开发者服务器。 | ✓ | ✓ |
| [my.downloadFile](api/xr054r) | 下载文件资源到本地。 | ✓ | ✓ |
| [my.connectSocket](api/vx19c3) | 创建一个 [WebSocket](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket) 的连接。 | ✓ | ✓ |
| [my.onSocketOpen](api/itm5og) | 监听 WebSocket 连接打开事件。 | ✓ | ✓ |
| [my.offSocketOpen](api/dva3t8) | 取消监听 WebSocket 连接打开事件。 | ✓ | ✓ |
| [my.onSocketError](api/giu3c2) | 监听 WebSocket 错误。 | ✓ | ✓ |
| [my.offSocketError](api/kk7vv7) | 取消监听 WebSocket 错误。 | ✓ | ✓ |
| [my.sendSocketMessage](api/mr91d1) | 通过 WebSocket 连接发送数据。 | ✓ | ✓ |
| [my.onSocketMessage](api/gecnap) | 监听 WebSocket 接受到服务器的消息事件。 | ✓ | ✓ |
| [my.offSocketMessage](api/roziyq) | 取消监听 WebSocket 接受到服务器的消息事件。 | ✓ | ✓ |
| [my.closeSocket](api/network) | 关闭 WebSocket 连接。 | ✓ | ✓ |
| [my.onSocketClose](api/foqk6g) | 监听 WebSocket 关闭。 | ✓ | ✓ |
| [my.offSocketClose](api/qc4q3t) | 取消监听WebSocket关闭。 | ✓ | ✓ |


# 设备

## 系统信息
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getSystemInfo](api/system-info) | 获取手机系统信息。 | ✓ | ✓ |
| [my.getSystemInfoSync](api/gawhvz) | 获取手机系统信息的同步接口。 | ✓ | ✓ |


## 网络状态
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getNetworkType](api/network-status) | 获取当前网络状态。 | ✓ | ✓ |
| [my.onNetworkStatusChange](api/ympi0l) | 开始网络状态变化的监听。 | ✓ | ✓ |
| [my.offNetworkStatusChange](api/gxpg1w) | 取消网络状态变化的监听。 | ✓ | ✓ |


## 剪切板
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getClipboard](https://opendocs.alipay.com/mini/api/clipboard) | 获取剪贴板数据。 | ✗ | ✓ |
| [my.setClipboard](https://opendocs.alipay.com/mini/api/klbkbp) | 设置剪贴板数据。 | ✗ | ✓ |


## 摇一摇
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.watchShake](api/shake) | 摇一摇功能。 | ✓ | ✓ |


## 振动
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.vibrate](api/vibrate) | 调用振动功能。 | ✓ | ✓ |
| [my.vibrateLong](api/ucm2he) | 较长时间的振动 (400ms)。 | ✓ | ✓ |
| [my.vibrateShort](api/ad6c10) | 较短时间的振动 (40ms)。 | ✓ | ✓ |


## 加速度计
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.startAccelerometer](https://opendocs.alipay.com/mini/022hgl) | 开始监听加速度数据。 | ✓ | ✓ |
| [my.stopAccelerometer](https://opendocs.alipay.com/mini/022hgm) | 停止监听加速度数据。 | ✓ | ✓ |
| [my.onAccelerometerChange](https://opendocs.alipay.com/mini/api/accelerometer) | 监听加速度数据。 | ✓ | ✓ |
| [my.offAccelerometerChange](https://opendocs.alipay.com/mini/api/kape7p) | 停止监听加速度数据。 | ✓ | ✓ |


## 陀螺仪
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.startGyroscope](https://opendocs.alipay.com/mini/022kkm) | 开始监听陀螺仪数据。 | ✓ | ✓ |
| [my.stopGyroscope](https://opendocs.alipay.com/mini/022hgn) | 停止监听陀螺仪数据。 | ✓ | ✓ |
| [my.onGyroscopeChange](https://opendocs.alipay.com/mini/api/gyroscope) | 监听陀螺仪数据变化事件。 | ✓ | ✓ |
| [my.offGyroscopeChange](https://opendocs.alipay.com/mini/api/cpt55i) | 停止监听陀螺仪数据。 | ✓ | ✓ |


## 罗盘
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.startCompass](https://opendocs.alipay.com/mini/022kkk) | 开始监听罗盘数据。 | ✓ | ✓ |
| [my.stopCompass](https://opendocs.alipay.com/mini/022kkl) | 停止监听罗盘数据。 | ✓ | ✓ |
| [my.onCompassChange](https://opendocs.alipay.com/mini/api/compass) | 监听罗盘数据。 | ✓ | ✓ |
| [my.offCompassChange](https://opendocs.alipay.com/mini/api/xf671t) | 停止监听罗盘数据。 | ✓ | ✓ |


## 设备方向
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.onDeviceMotionChange](https://opendocs.alipay.com/mini/api/my.ondevicemotionchange) | 监听设备方向变化。 | ✓ | ✓ |
| [my.offDeviceMotionChange](https://opendocs.alipay.com/mini/api/my.offdevicemotionchange) | 停止监听设备方向变化。 | ✓ | ✓ |


## 拨打电话
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.makePhoneCall](api/macke-call) | 拨打电话。 | ✓ | ✓ |


## 获取服务器时间
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getServerTime](api/get-server-time) | 获取当前服务器时间的毫秒数。 | ✓ | ✓ |


## 用户截屏事件
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.onUserCaptureScreen](api/user-capture-screen) | 监听用户发起的主动截屏事件。 | ✓ | ✓ |
| [my.offUserCaptureScreen](api/umdxbg) | 取消监听截屏事件。 | ✓ | ✓ |


## 屏幕亮度
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.setKeepScreenOn](api/qx0sap) | 设置是否保持屏幕长亮状态。 | ✓ | ✓ |
| [my.getScreenBrightness](api/screen-brightness) | 获取屏幕亮度。 | ✓ | ✓ |
| [my.setScreenBrightness](api/ccf32t) | 设置屏幕亮度。 | ✓ | ✓ |


## 设置
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.openSetting](api/qflu8f) | 打开小程序设置界面，返回用户权限设置的结果。 | ✓ | ✓ |
| [my.getSetting](/mini/api/xmk3ml) | 获取用户的当前设置。 | ✓ | ✓ |


## 添加手机联系人
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.addPhoneContact](/mini/api/contact) | 用户可以选择将该表单以“创建新联系人”或“添加到现有联系人”的方式，写入到手机系统的通讯录。 | ✓ | ✓ |


## 无障碍
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.isScreenReaderEnabled](https://opendocs.alipay.com/mini/api/device/isscreenreaderenabled) | 获取设备是否开启无障碍模式。 | ✗ | ✓ |


## 权限引导
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.showAuthGuide](/mini/api/show-auth-guide) | 通过权限引导模块以图文等形式向用户弹出 Dialog，引导用户打开相应的权限。 | ✓ | ✓ |


## 扫码
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.scan](/mini/api/scan) | 调用扫一扫功能。 | ✓ | ✓ |


## 内存不足告警
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.onMemoryWarning](api/rb9o8p) | 开始监听内存不足的告警事件。 | ✓ | ✓ |
| [my.offMemoryWarning](api/hszexr) | 停止监听内存不足的告警事件。 | ✓ | ✓ |


## 获取设备电量
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getBatteryInfo](api/nrnziy) | 获取电量的异步接口。 | ✗ | ✓ |
| [my.getBatteryInfoSync](api/vf7vn3) | 获取电量的同步接口。 | ✗ | ✓ |


## 蓝牙
| **名称** | **功能说明** |
| --- | --- |
| [蓝牙 API 错误码对照表](https://opendocs.alipay.com/mini/api/ucd2lh) | 罗列蓝牙 API 相关错误码信息与解决方案，方便用户依表查询。 |
| [蓝牙 API FAQ](https://opendocs.alipay.com/mini/0090tx) | 对蓝牙 API 的常见问题解答。 |


### 低功耗蓝牙
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.connectBLEDevice](api/tmew6e) | 连接低功耗蓝牙设备。 | ✗ | ✓ |
| [my.setBLEMTU](https://opendocs.alipay.com/mini/api/my.setblemtu) | 设置低功耗蓝牙设备最大传输单元（MTU）。需在 [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) 调用成功后调用，mtu 设置范围（22, 512）。 | ✗ | ✓ |
| [my.getBLEMTU](https://opendocs.alipay.com/mini/api/my.getblemtu) | 获取低功耗蓝牙设备的最大传输单元（MTU）。 | ✗ | ✓ |
| [my.disconnectBLEDevice](api/yqrmmk) | 断开与低功耗蓝牙设备的连接。 | ✗ | ✓ |
| [my.writeBLECharacteristicValue](api/vmp2r4) | 向低功耗蓝牙设备特征值中写入数据。 | ✗ | ✓ |
| [my.readBLECharacteristicValue](api/zro0ka) | 读取低功耗蓝牙设备特征值中的数据。 | ✗ | ✓ |
| [my.notifyBLECharacteristicValueChange](api/pdzk44) | 启用低功耗蓝牙设备特征值变化时的 notify 功能。 | ✗ | ✓ |
| [my.getBLEDeviceServices](api/uzsg75) | 获取蓝牙设备所有 service（服务）。 | ✗ | ✓ |
| [my.getBLEDeviceRSSI](https://opendocs.alipay.com/mini/api/my.getbledevicerssi) | 获取蓝牙低功耗设备的信号强度（Received Signal Strength Indication, RSSI）。 | ✗ | ✓ |
| [my.getBLEDeviceCharacteristics](api/fmg9gg) | 获取蓝牙设备所有 characteristic（特征值）。 | ✗ | ✓ |
| [my.onBLECharacteristicValueChange](api/cdu501) | 监听低功耗蓝牙设备的特征值变化的事件。 | ✗ | ✓ |
| [my.offBLECharacteristicValueChange](api/dlxobk) | 监听低功耗蓝牙设备的特征值变化的事件。 | ✗ | ✓ |
| [my.onBLEConnectionStateChanged](api/utgyiu) | 监听低功耗蓝牙连接的错误事件，包括设备丢失，连接异常断开等。 | ✗ | ✓ |
| [my.offBLEConnectionStateChanged](api/xfuy7k) | 取消低功耗蓝牙连接状态变化事件的监听。 | ✗ | ✓ |


### 传统蓝牙
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.openBluetoothAdapter](api/kunuy4) | 初始化小程序蓝牙模块。 | ✗ | ✓ |
| [my.closeBluetoothAdapter](api/wvko0w) | 关闭本机蓝牙模块。 | ✗ | ✓ |
| [my.getBluetoothAdapterState](api/eid4o6) | 获取本机蓝牙模块状态。 | ✗ | ✓ |
| [my.startBluetoothDevicesDiscovery](api/ksew43) | 获取本机蓝牙模块状态。 | ✗ | ✓ |
| [my.stopBluetoothDevicesDiscovery](api/syb4mi) | 停止搜寻附近的蓝牙外围设备。 | ✗ | ✓ |
| [my.getBluetoothDevices](api/pelizr) | 获取所有已发现的蓝牙设备，包括已经和本机处于连接状态的设备。 | ✗ | ✓ |
| [my.getConnectedBluetoothDevices](api/ge8nue) | 获取处于已连接状态的设备。 | ✗ | ✓ |
| [my.onBluetoothDeviceFound](api/mhzls9) | 搜索到新的蓝牙设备时触发此事件。 | ✗ | ✓ |
| [my.offBluetoothDeviceFound](api/snw2t7) | 移除寻找到新的蓝牙设备事件的监听。 | ✗ | ✓ |
| [my.onBluetoothAdapterStateChange](api/eegfbk) | 监听本机蓝牙状态变化的事件。 | ✗ | ✓ |
| [my.offBluetoothAdapterStateChange](api/ocgwfe) | 移除本机蓝牙状态变化的事件的监听。 | ✗ | ✓ |
| [my.makeBluetoothPair](https://opendocs.alipay.com/mini/api/makebluetoothpair) | 蓝牙配对接口。连接蓝牙之前，部分设备需要先配对。 | ✗ | ✓ |
| [my.cancelBluetoothPair](https://opendocs.alipay.com/mini/01zarv) | 取消蓝牙设备配对。 | ✗ | ✓ |
| [my.getBluetoothPairs](https://opendocs.alipay.com/mini/01zdnf) | 获取已经配对的蓝牙设备。  | ✗ | ✓ |


### iBeacon
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.startBeaconDiscovery](api/cy1g7k) | 开始搜索附近的 iBeacon 设备。 | ✗ | ✓ |
| [my.stopBeaconDiscovery](api/yp5owa) | 停止搜索附近的 iBeacon 设备。 | ✗ | ✓ |
| [my.getBeacons](api/yqleyc) | 获取已经搜索到的 iBeacon 设备。 | ✗ | ✓ |
| [my.onBeaconUpdate](api/kvdg9y) | 监听 iBeacon 设备的更新事件。 | ✗ | ✓ |
| [my.onBeaconServiceChange](api/rq1dl7) | 监听 iBeacon 服务的状态变化。 | ✗ | ✓ |
| [my.offBeaconServiceChange](https://opendocs.alipay.com/mini/api/offbeaconservicechange) | 取消监听 iBeacon 服务的状态变化。 | ✗ | ✓ |
| [my.offBeaconUpdate](https://opendocs.alipay.com/mini/api/offbeaconupdate) | 取消监听 iBeacon 设备的更新事件。 | ✗ | ✓ |


# worker
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createWorker](https://opendocs.alipay.com/mini/api/createworker) | 创建一个 Worker 线程。 | ✗ | ✓ |


# 数据安全
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.rsa](/mini/api/data-safe) | 非对称加密。 | ✓ | ✓ |


# 分享
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [onShareAppMessage](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0) | 在 Page 中定义 onShareAppMessage 函数，设置该页面的分享信息。 | ✓ | ✓ |
| [my.hideShareMenu](/mini/api/share_app) | 隐藏分享按钮。 | ✓ | ✓ |
| [my.showSharePanel](api/omg2ye) | 唤起分享面板。 | ✓ | ✓ |


# 自定义通用菜单
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.hideAddToDesktopMenu](/mini/api/optionmenuitem) | 隐藏当前页面通用菜单中的 **添加到桌面** 功能。 | ✓ | ✓ |
| [my.hideAllAddToDesktopMenu](api/fdaplu) | 隐藏所有页面的通用菜单中的 **添加到桌面** 功能。 | ✓ | ✓ |


# 更新管理
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getUpdateManager](api/zdblqg) | 创建一个 UpdateManager 对象，获取全局唯一的版本更新管理器，用于管理小程序更新。 | ✗ | ✓ |
| [UpdateManager](api/ngwgfi) | UpdateManager 对象，用来管理更新，可通过 my.getUpdateManager 接口获取实例。 | ✗ | ✓ |


# web-view 组件控制
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.createWebViewContext](/mini/api/webview-context) | 通过创建`webviewContext`提供从小程序向`web-view`发送消息的能力。创建并返回 `web-view` 上下文 `webViewContext` 对象。 | ✗ | ✓ |


# 跳转支付宝应用或页面
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.ap.navigateToAlipayPage](/mini/api/navigatetoalipaypage) | 小程序中跳转到支付宝官方业务或运营活动页面。 | ✓ | ✓ |


# 升级支付宝最新版本
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.ap.updateAlipayClient](api/updatealipayclient) | 打开支付宝客户端升级界面。 | ✓ | ✓ |


# 开放能力 API

## 基础能力
| **能力名称** | **API 名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- | --- |
| [小程序相互跳转](https://opendocs.alipay.com/mini/introduce/open-miniprogram) | [my.navigateBackMiniProgram](https://opendocs.alipay.com/mini/api/open-miniprogram) | 跳转回上一个小程序的 API，只有当另一个小程序跳转到当前小程序时才能调用成功。 | ✓ | ✓ |
|  | [my.navigateToMiniProgram](https://opendocs.alipay.com/mini/api/yz6gnx) | 跳转到其他小程序。 | ✓ | ✓ |
|  | [小程序相互跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4) | 对小程序相互跳转的常见问题解答。 | - | - |
| [用户授权](https://docs.alipay.com/mini/introduce/authcode) | [my.getAuthCode](https://docs.alipay.com/mini/api/openapi-authorize) | 获取用户授权码。 | ✓ | ✓ |
|  | [用户授权 FAQ](https://opendocs.alipay.com/mini/api/bpubha) |  | - | - |


## 支付能力
| **能力名称** | **API 名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- | --- |
| [小程序支付](https://opendocs.alipay.com/mini/introduce/pay) | [my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | 小程序唤起支付。 | ✗ | ✓ |
|  | [小程序支付 / 资金授权 FAQ](https://opendocs.alipay.com/mini/api/tmz0kq) |  | - | - |


## 资金能力
| **能力名称** | **API 名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- | --- |
| [资金授权](https://opendocs.alipay.com/mini/introduce/pre-authorization) | [my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | 小程序支付接口。 | ✗ | ✓ |
|  | [小程序支付 / 资金授权 FAQ](https://opendocs.alipay.com/mini/api/tmz0kq) |  | - | - |
| [周期扣款](https://opendocs.alipay.com/mini/006srl) | [my.paySignCenter](https://opendocs.alipay.com/mini/006v6d) | 在支付宝小程序内启动一个代扣 H5 服务。 | ✗ | ✓ |


## 会员能力
| **能力名称** | **API 名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- | --- |
| [获取会员基础信息](https://opendocs.alipay.com/mini/introduce/twn8vq) | [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize) | 用户授权获取授权 code。注意在此注册流程中，scopes 参数请传递 “auth_base”。 | ✓ | ✓ |
|  | [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) | 获取会员基础信息。 | ✓ | ✓ |
|  | [获取会员基础信息 FAQ](https://opendocs.alipay.com/mini/api/qcn29g) |  | - | - |
| [获取会员手机号](https://opendocs.alipay.com/mini/introduce/getphonenumber) | [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) | 获取会员手机号码。 | ✗ | ✓ |
|  | [获取会员手机号 FAQ](https://opendocs.alipay.com/mini/api/dwou7f) |  | - | - |
| [获取会员收货地址](https://opendocs.alipay.com/mini/introduce/getaddress) | [my.getAddress](https://opendocs.alipay.com/mini/api/lymgfk) | 获取会员收货地址。 | ✗ | ✓ |
| [商户会员卡](https://opendocs.alipay.com/mini/introduce/card) | [my.addCardAuth](https://opendocs.alipay.com/mini/api/add-card-auth) | 小程序内唤起开卡页面。 | ✗ | ✓ |
|  | [my.openCardList](https://opendocs.alipay.com/mini/api/qxxpsh) | 打开支付宝卡包中的“卡”列表。 | ✗ | ✓ |
|  | [my.openMerchantCardList](https://opendocs.alipay.com/mini/api/axfplw) | 打开当前用户领取某个商户的“卡”列表。 | ✗ | ✓ |
|  | [my.openCardDetail](https://opendocs.alipay.com/mini/api/card-voucher-ticket#myopencarddetail) | 打开当前用户领取某张卡的详情页。 | ✗ | ✓ |


## 营销能力
| **能力名称** | **API 名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- | --- |
| [支付宝卡包](https://opendocs.alipay.com/mini/introduce/voucher) | [my.openVoucherList](https://opendocs.alipay.com/mini/api/vq3mgn) | 打开支付宝卡包中的“劵”列表。 | ✗ | ✓ |
|  | [my.openMerchantVoucherList](https://opendocs.alipay.com/mini/api/sgvgu6) | 打开当前用户领取某个商户的“劵”列表。 | ✗ | ✓ |
|  | [my.openVoucherDetail](https://opendocs.alipay.com/mini/api/card-voucher-ticket#myopenvoucherdetail) | 打开当前用户领取某张劵的详情页（非口碑劵）。 | ✗ | ✓ |
|  | [my.openKBVoucherDetail](https://opendocs.alipay.com/mini/api/ga4obi) | 打开当前用户领取某张劵的详情页（口碑劵）。 | ✗ | ✓ |
|  | [my.openTicketList](https://opendocs.alipay.com/mini/api/ezt6u3) | 打开支付宝卡包中的“票”列表。 | ✗ | ✓ |
|  | [my.openMerchantTicketList](https://opendocs.alipay.com/mini/api/yee76y) | 打开当前用户领取某个商户的“票”列表。 | ✗ | ✓ |
|  | [my.openTicketDetail](https://opendocs.alipay.com/mini/api/ry7ftz) | 打开当前用户领取某张票的详情页。 | ✗ | ✓ |
| [运动数据](https://opendocs.alipay.com/mini/introduce/rundata) | [my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v) | 获取步数。 | ✗ | ✓ |
| [小程序自定义分享](https://opendocs.alipay.com/mini/introduce/share) | [onShareAppMessage](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0) | 设置页面的分享信息。 | ✓ | ✓ |


## 安全能力
| **能力名称** | **API 名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- | --- |
| [先享后付保障](https://opendocs.alipay.com/mini/introduce/non-sufficient-funds) | [my.ap.nsf](https://opendocs.alipay.com/mini/api/nsf) | 先享后付保障。 | ✗ | ✓ |
| [营销反作弊](https://opendocs.alipay.com/mini/introduce/antimarketcheat) | [my.ap.preventCheat](https://opendocs.alipay.com/mini/api/antimarketcheat) | 营销反作弊。 | ✗ | ✓ |
| [文本风险识别](https://opendocs.alipay.com/mini/introduce/text-identification) | [my.textRiskIdentification](https://opendocs.alipay.com/mini/api/text-identification) | 文本风险识别（用户端）。 | ✗ | ✓ |
| [图片内容安全](https://opendocs.alipay.com/mini/introduce/img_risk) | [my.ap.imgRisk](https://opendocs.alipay.com/mini/api/img_risk) | 图片提交接口。 | ✗ | ✓ |
|  | [my.ap.imgRiskCallback](https://opendocs.alipay.com/mini/api/ze6675) | 风险结果查询接口。 | ✗ | ✓ |


# 模板配置
| **名称** | **功能说明** | **支持个人支付宝小程序** | **支持企业支付宝小程序** |
| --- | --- | --- | --- |
| [my.getExtConfig](https://opendocs.alipay.com/mini/api/getExtConfig) | 获取 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 自定义数据字段的异步接口。 | ✗ | ✓ |
| [my.getExtConfigSync](https://opendocs.alipay.com/mini/api/getExtConfigSync) | 获取 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 自定义数据字段的同步接口。 | ✗ | ✓ |



