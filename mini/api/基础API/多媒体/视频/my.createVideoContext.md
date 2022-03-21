
# 简介
**my.createVideoContext** 是传入 video id，返回一个 videoContext 上下文的 API。video id 为开发者在对应 video 标签中自由命名的 ID 属性。

通过 videoContext 可以操作一个 [video 组件](https://opendocs.alipay.com/mini/component/video)。更多信息，请参见 [视频播放](https://opendocs.alipay.com/mini/introduce/video)。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，可查看 [接入准备](https://opendocs.alipay.com/mini/02p2m1)。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验
![|127x157](https://cdn.nlark.com/yuque/0/2021/png/179989/1625192981193-ef7ee1bf-0e3e-4231-a5aa-5f88c3bce9c8.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&name=1.png&originHeight=157&originWidth=127&size=15042&status=done&style=stroke&width=127)

## 效果示例
![|300x601](https://cdn.nlark.com/yuque/0/2021/png/179989/1625192989668-e8bee3e5-3c24-4ef3-8b29-505d5d510841.png#align=left&display=inline&height=601&margin=%5Bobject%20Object%5D&name=2.png&originHeight=601&originWidth=300&size=111477&status=done&style=stroke&width=300)

# 接口调用

## 示例代码
开发者在 .axml 文件中写入如下代码，命名 video id。video id 为开发者在对应 video 标签中自由命名的 ID 属性，例如下方代码中的 myVideo 。
```html
<view>
<!-- onPlay 的类型是 EventHandle。为当开始/继续播放时触发 play 事件。 -->
  <video id="myVideo" src="{{src}}" onPlay="{{onPlay}}" enableNative="{{true}}"></video>
   <button type="default" size="defaultSize" onTap="play"> Play </button>
   <button type="default" size="defaultSize" onTap="pause"> Pause </button>
   <button type="default" size="defaultSize" onTap="stop"> stop </button>
   <button type="default" size="defaultSize" onTap="seek"> seek </button>
   <button type="default" size="defaultSize" onTap="requestFullScreen"> requestFullScreen </button>
   <button type="default" size="defaultSize" onTap="exitFullScreen"> exitFullScreen </button>
   <button type="default" size="defaultSize" onTap="mute"> mute </button>
   <button type="default" size="defaultSize" onTap="playbackRate"> playbackRate </button>
</view>
```
﻿开发者在 .js 文件中写入如下代码：
```javascript
Page({
  data: {

  // src 为要播放的视频资源地址，支持优酷视频编码（支付宝客户端 10.1.75）。src 支持的协议如下：vid/showId: XMzg2Mzc5MzMwMA== apFilePath: https://resource/xxx.video。
    src: "XNDM0OTQzMDc2OA==",
  },
  onLoad() {
    this.videoContext = my.createVideoContext('myVideo');
  },
  play() {
    this.videoContext.play();
  },
  pause() {
    this.videoContext.pause();
  },
  stop() {
    this.videoContext.stop();
  },
  seek() {
    this.videoContext.seek(100);
  },
  requestFullScreen() {
    this.videoContext.requestFullScreen({
      direction: 0
    });
  },
  exitFullScreen() {
    this.videoContext.exitFullScreen();
  },
  mute() {
    this.videoContext.mute(false);
  },
  playbackRate() {
    this.videoContext.playbackRate(1.5);
  },
});
```

### videoContext 方法列表
| **方法** | **参数** | **类型** | **描述** |
| --- | --- | --- | --- |
| play | 无 | - | 播放。 |
| pause | 无 | - | 暂停。 |
| stop | 无 | - | 停止。 |
| seek | position | Number | 跳转到指定位置，单位为秒（s）。 |
| requestFullScreen | direction | Number | 进入全屏。<li>0 为正常竖屏。</li><li>90 为横屏。</li><li>-90 为反向横屏。</li>|
| exitFullScreen | 无 | - | 退出全屏。 |
| showStatusBar | 无 | - | 显示状态栏，仅在 iOS 全屏下有效。 |
| hideStatusBar | 无 | - | 隐藏状态栏，仅在 iOS 全屏下有效。 |
| mute | ison | Boolean | 切换静音状态。 |
| playbackRate | rate | Number | 设置倍速播放 （0.5 <= rate <= 2.0）。 |
| showFloatingWindow | isShow | Boolean | 显示/隐藏浮窗，如 showFloatingWindow(false); |


## 错误码
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
| 1023 | 播放中内部错误（FFmpeg 内错误）。 | 检查 FFmpeg。 |
| 2004 | 播放过程中加载时间超时。 | 检查并重试。 |
| 3001 | audio 渲染出错。 | 检查 audio 渲染。 |
| 3002 | 硬解码错误。 | 检查硬解码。 |


# 支持格式

## 支持的视频封装格式
iOS、Android 支持以下视频封装格式： MP4、mov、m4v、3gp、m3u8、flv 。

## 支持的编码格式
iOS、Android 支持以下编码格式： H.264、AAC。

