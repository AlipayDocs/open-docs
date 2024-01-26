# 简介

用户可通过 video 组件播放视频，目前暂只支持优酷渠道上传的视频及网络地址的视频，获取[优酷视频码指南](https://opendocs.alipay.com/mini/081db1)。相关 API：[my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext)。

## 使用限制

- 支持基础库版本 1.10.0 及以上，低版本需要做 [兼容处理](/mini/framework/compatibility)。
- 不支持 css 动画，使用无效。
- 自定义竖屏观看视频时两边出现的白色填充：
  - 如果是因为视频的宽高比跟 video 组件的宽高比不一致，请通过 object-fit 进行调整 。
  - 如果是由于 poster 实际的宽高比跟容器的宽高比不一致，请通过 poster-size 进行调整。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ffcb08caac192788a1dcae326da38bbf.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

## 效果示例

<img src="https://img.alicdn.com/imgextra/i3/O1CN01IjNIk21RhzwrrI5c3_!!6000000002144-2-tps-738-1486.png" width="300" height="601"/>

# 使用

## 示例代码

### .axml 示例代码

```html
<view>
  <video
    id="myVideo"
    src="{{video.src}}"
    controls="{{video.showAllControls}}"
    loop="{{video.isLooping}}"
    muted="{{video.muteWhenPlaying}}"
    show-fullscreen-btn="{{video.showFullScreenButton}}"
    show-play-btn="{{video.showPlayButton}}"
    show-center-play-btn="{{video.showCenterButton}}"
    object-fit="{{video.objectFit}}"
    autoplay="{{video.autoPlay}}"
    direction="{{video.directionWhenFullScreen}}"
    initial-time="{{video.initTime}}"
    mobilenet-hint-type="{{video.mobilenetHintType}}"
    onPlay="onPlay"
    onPause="onPause"
    onEnded="onEnded"
    onError="onPlayError"
    onTimeUpdate="onTimeUpdate"
  />
</view>
```

### .js 示例代码

```javascript
Page({
  data: {
    status: 'inited',
    time: '0',
    video: {
      src: 'XNDM0OTQzMDc2OA==',
      showAllControls: false,
      showPlayButton: false,
      showCenterButton: true,
      showFullScreenButton: true,
      isLooping: false,
      muteWhenPlaying: false,
      initTime: 0,
      objectFit: 'contain',
      autoPlay: false,
      directionWhenFullScreen: 90,
      mobilenetHintType: 2,
    },
  },
  onPlay(e) {
    console.log('onPlay');
  },
  onPause(e) {
    console.log('onPause');
  },
  onEnded(e) {
    console.log('onEnded');
  },
  onPlayError(e) {
    console.log('onPlayError, e=' + JSON.stringify(e));
  },
  onTimeUpdate(e) {
    console.log('onTimeUpdate:', e.detail.currentTime);
  },
});
```

## 属性说明

>  表格中 “-” 代表支持。 


| **属性** | **类型** | **描述** | **WebView</br>兼容性** |**Native</br>兼容性** |
| --- | --- | --- | -------------- | -------------- |
| style | String | 内联样式。 | - | - |
| class | String | 外部样式名。 | - | - |
| src | String | 要播放视频的资源地址，支持网络地址，支持优酷视频编码（支付宝客户端 10.1.75）。<br />src 支持的协议如下：<br />vid/showId: XMzg2Mzc5MzMwMA==<br />apFilePath: `https://resource/xxx.video`。 | - | - |
| poster | String | 视频封面图的 url，支持 jpg、png 等图片，如 `https://***.jpg`。如果不传的话，默认取视频的首帧图作为封面图。 | - | - |
| poster-size | String | 当 poster 高宽比跟视频高宽不匹配时，如何显示 poster，设置规则同 background-size 一致。<br />**默认值：** contain | - | - |
| object-fit | String | 当视频大小与 video 容器大小不一致时，视频的表现形式。contain：包含，fill：填充。<br />**默认值：** contain | - | - |
| initial-time | Number | 指定视频初始播放位置，单位 s。 | 基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| duration | Number | 为无法读取时长的视频设置时长，单位 s。 | - | - |
| controls | Boolean | 是否显示默认播放控件（底部工具条，包括播放/暂停按钮、播放进度、时间）。<br />**默认值：** true | - | - |
| autoplay | Boolean | 是否自动播放。<br />**默认值：** false | - | - |
| direction | Number | 设置全屏时视频的方向，不指定则根据宽高比自动判断。有效值为 0（正常竖向）, 90（屏幕逆时针 90 度）, -90（屏幕顺时针 90 度） | 基础库 [1.12.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| loop | Boolean | 是否循环播放。<br />**默认值：** false | 基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| muted | Boolean | 是否静音播放。<br />**默认值：** false | 基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| show-fullscreen-btn | Boolean | 是否显示全屏按钮。<br />**默认值：** true | 基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| show-play-btn | Boolean | 是否显示视频底部控制栏的播放按钮。<br />**默认值：** true | 基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| show-center-play-btn | Boolean | 是否显示视频中间的播放按钮。<br />**默认值：** true | 基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| show-mute-btn | Boolean | 是否展示工具栏上的静音按钮。<br />**默认值：** true | 基础库 [1.13.7+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| show-thin-progress-bar | Boolean | 当底部工具条隐藏时，是否显示细进度条（controls=false 时设置无效）。<br />**默认值：** false | 基础库 [1.15.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| enable-progress-gesture | Boolean | 全屏模式下是否开启控制进度的手势。<br />**默认值：** false |基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| mobilenet-hint-type | Number | 移动网络提醒样式。<br /> <ul><li>0 - 不提醒</li><li>1 - tip 提醒</li><li>2 - 阻塞提醒(无消耗流量大小)</li><li>3 - 阻塞提醒(有消耗流量大小提醒)</li></ul><br />**默认值：** 1 | 基础库 [1.13.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| onPlay | EventHandle | 当开始/继续播放时触发 play 事件。 | - | - |
| onPause | EventHandle | 当暂停播放时触发 pause 事件。 | - | - |
| onEnded | EventHandle | 当播放到末尾时触发 ended 事件。 | - | - |
| onTimeUpdate | EventHandle | 播放进度变化时触发，`event.detail = {currentTime: '当前播放时间',userPlayDuration:'用户实际观看时长',videoDuration:'视频总时长'}`。 | 基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility)  | - |
| onLoading | EventHandle | 视频出现缓冲时触发。 | - | - |
| onError | EventHandle | 视频播放出错时触发（errorCode 见下面错误码表）。 | - | - |
| onFullScreenChange | EventHandle | 视频进入和退出全屏时触发，`event.detail = {fullScreen, direction}`，direction 取为 vertical 或 horizontal。 | 基础库 [1.12.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| onTap | EventHandle | 点击视频 view 时触发，`event.detail = {ptInView:{x:0,y:0}}`。 | - | - |
| onUserAction | EventHandle | 用户操作事件，event.detail = {tag:"mute", value:0}，tag 为用户操作的元素，目前支持的 tag 有：play（底部播放按钮）、centerplay（中心播放按钮）、mute（静音按钮）、fullscreen（全屏按钮）、retry（重试按钮）、mobilenetplay（网络提醒的播放按钮）。 | - | - |
| onStop | EventHandle | 视频播放终止。 | 基础库 [1.9.0+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| onRenderStart | EventHandle | 当视频加载完真正开始播放时触发。 | 基础库 [1.13.6+](https://opendocs.alipay.com/mini/framework/compatibility) | - |
| floating-mode | String | 浮窗设置。暂时不支持全局浮窗。<br />**可选值**：<br /><ul><li>none：无浮窗。</li><li>page：页面内浮窗。</li>miniprogram：跨页面浮窗。</li></ul> **默认值**：none | 基础库 [1.24.6+](https://opendocs.alipay.com/mini/framework/compatibility) | 暂不支持 |

### 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 1 | 未知错误。 | - |
| 400 | 读 ups 信息超时。 | 检查读 ups 信息。 |
| 1002 | 播放器内部错误。 | 检查播放器内部。 |
| 1005 | 网络连接失败。 | 检查网络连接。 |
| 1006 | 数据源错误。 | 检查数据源。 |
| 1007 | 播放器准备失败。 | 检查播放器。 |
| 1008 | 网络错误。 | 检查网络。 |
| 1009 | 搜索视频出错（源出错的一种）。 | 检查源。 |
| 1010 | 准备超时，也可认为是网络太慢或数据源太慢导致的播放失败。 | 检查是否因网络或数据原因导致的超时错误。 |
| 1023 | 播放中内部错误（FFmpeg 错误）。 | 检查资源是否符合标准，具体可参考本文中的“支持格式”小节。 |
| 2004 | 播放过程中加载时间超时。 | 检查并重试。 |
| 3001 | audio 渲染出错。 | 检查音频资源是否符合标准。 |
| 3002 | 硬解码错误。 | 检查设备的硬解码功能是否正常。 |

### 支持的视频封装格式

iOS、Android 支持以下视频封装格式： mp4、mov、m4v、3gp、m3u8、flv。

### 支持的编码格式

iOS、Android 支持以下编码格式： H.264、H.265、AAC。

# FAQ

### video 组件中播放的视频，当用户加载观看视频一次后，再次进行观看的时候是拉取的缓存，还是再次使用网络重新加载的？

目前的缓存策略是如果视频是循环播放的，再次观看是拉取的缓存，如果不是循环播放，每次都是网络重新加载。 主要是针对一些循环播放的短视频场景提供缓存能力。

### 缓存中的视频什么时候会清除掉 ？

页面销毁或者关闭小程序会清除掉。

### 小程序如何获取视频时长？

在视频组件 onTimeUpdate 方法中获取。

### video 组件，把 loop 字段设置为循环播放，在播放第二次的时候，把视频资源删除，发现无法播放 ？

虽然再次播放拉取的是缓存中的视频，但是还是会校验视频资源的。

### 出现异常问题自查步骤

- 原始 AXML 中是否包含三要素【id="main-map"】【class="nbcomponentanimation-main-map"】【<param name="id" value="main-map">】
- id 不能为【drawing area root】【content root】【RenderView】【TileGrid container】【Page TiledBacking containment】【ancestor clipping】等保留关键字
- id 不能包含一些特殊字符，如【 \* 】【 / 】，保证为大小写字母【 - 】【 \_ 】组成
- id 长度最好保持适中，不要以当前小程序 id、当前 unix 时间戳作为部分内容，导致 id 过长
- 保证 id 关键字在 AXML 的唯一性，若 id 为【main-map】，请尽量不要出现【main-map-wapper】类似的 id 值，可能会生成 WKCompositingView 导致同层组件添加位置出错
- 可以尝试 `raw-controls`属性，可解决 h5 的 video 组件在支付宝容器内出现层级过高的问题
