# 简介

**my.createVideoContext** 是传入 video id，返回一个 videoContext 上下文的 API。video id 为开发者在对应 video 标签中自由命名的 id 属性。

通过 videoContext 可以操作一个 [video 视频](https://opendocs.alipay.com/mini/component/video) 组件。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 仅支持播放优酷视频，开发者需要在优酷 **上传视频** 以获取视频码。
- 此 API 暂仅支持企业支付宝小程序使用。

### 支持格式

#### 支持的视频封装格式

iOS、Android 支持以下视频封装格式： MP4、mov、m4v、3gp、m3u8、flv 。

#### 支持的编码格式

iOS、Android 支持以下编码格式： H.264、AAC。

### 上传视频限制

- 上传的视频内容必须符合优酷相关规定。
- 视频内容需健康文明，相关规定可查看 [小程序违规处理规则](https://opendocs.alipay.com/rules/rules_mini/nowgsa)。若发布后内容涉及违规，支付宝将根据小程序服务协议、本规则及相应细则对视频、开发者以及小程序采取相应管理措施。

## 扫码体验

![|127x157](https://cdn.nlark.com/yuque/0/2021/png/179989/1625192981193-ef7ee1bf-0e3e-4231-a5aa-5f88c3bce9c8.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&name=1.png&originHeight=157&originWidth=127&size=15042&status=done&style=stroke&width=127)

## 效果示例

<img src="https://img.alicdn.com/imgextra/i3/O1CN01IjNIk21RhzwrrI5c3_!!6000000002144-2-tps-738-1486.png" width="300" height="601"/>

# 上传视频获取视频码

1. 访问 [优酷视频上传](https://mp.youku.com/new/upload_home) 页面，并使用开发小程序的 **支付宝主账号** 扫码登录，**否则视频无法上传，则无法获取到视频编码及定向支付宝小程序播放的设置**。 ![1.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1655905047219-3eaa58fc-ce22-44c5-887a-89f8a7a582f5.png#align=left&display=inline&height=937&margin=%5Bobject%20Object%5D&name=1.png&originHeight=937&originWidth=1920&size=546709&status=done&style=none&width=1920)
2. 登录成功后，上传视频文件。 ![2.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1655905058699-82942894-c24e-41e2-9da8-b7386a526e31.png#align=left&display=inline&height=732&margin=%5Bobject%20Object%5D&name=2.png&originHeight=732&originWidth=1500&size=185998&status=done&style=none&width=1500)
3. 配置 **隐私设置** 为 **仅小程序可播**（不对优酷用户开放此视频），开发者根据所传视频如实填写视频简介等其它信息（建议填写完整，避免出现审核不通过的情况），点击 **保存发布**。 ![3.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1655905072410-92740442-13d4-46a6-a36a-950dcca90367.png#align=left&display=inline&height=732&margin=%5Bobject%20Object%5D&name=3.png&originHeight=732&originWidth=1500&size=232376&status=done&style=none&width=1500)
4. 提交上传视频后耐心等待视频审，开发者上传的视频需要符合优酷审核标准。审核时间约为一个工作日，开发者如对审核进度和审核结果有疑问可以拨打优酷客服电话 400-810-3568 咨询。 ![4.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1655905086801-15768829-9302-4ae0-b303-4cb2f90a55b4.png#align=left&display=inline&height=732&margin=%5Bobject%20Object%5D&name=4.png&originHeight=732&originWidth=1500&size=185956&status=done&style=none&width=1500)
5. 上传视频通过审核后，开发者进入 **视频管理** 页面，点击播放后在浏览器地址栏找到播放地址，其中 `v_show/id_` 之后的部分则为视频码。例如：`https://v.youku.com/v_show/id_XNDU0MTM4NjQxLl==.html` 中，`XNDU0MTM4NjQxLl==`即为视频码。

# 接口调用

## 示例代码

### .axml 示例代码

开发者在 .axml 文件中写入如下代码。其中 video id 为开发者在对应 video 标签中自由命名的 id 属性，例如下方代码中的 `myVideo`；src 属性中需传入优酷视频的视频码进行播放。

```html
<view>
  <!-- onPlay 的类型是 EventHandle。为当开始/继续播放时触发 play 事件。 -->
  <video
    id="myVideo"
    src="{{src}}"
    onPlay="{{onPlay}}"
    enableNative="{{true}}"
  ></video>
  <button type="default" size="defaultSize" onTap="play">Play</button>
  <button type="default" size="defaultSize" onTap="pause">Pause</button>
  <button type="default" size="defaultSize" onTap="stop">stop</button>
  <button type="default" size="defaultSize" onTap="seek">seek</button>
  <button type="default" size="defaultSize" onTap="requestFullScreen">
    requestFullScreen
  </button>
  <button type="default" size="defaultSize" onTap="exitFullScreen">
    exitFullScreen
  </button>
  <button type="default" size="defaultSize" onTap="mute">mute</button>
  <button type="default" size="defaultSize" onTap="playbackRate">
    playbackRate
  </button>
  <button type="default" size="defaultSize" onTap="enterPicture">进入画中画</button>
  <button type="default" size="defaultSize" onTap="exitPicture">退出进入画中画</button>
</view>
```

### .js 示例代码

开发者在 .js 文件中写入如下代码：

```javascript
Page({
  data: {
    // src 为要播放的视频资源地址，支持优酷视频编码（支付宝客户端 10.1.75）。
    // src 支持的协议如下：
    // 1. vid/showId: XMzg2Mzc5MzMwMA==
    // 2. tempFilePath (本地缓存文件): https://resource/xxx.video
    src: 'XNDM0OTQzMDc2OA==',
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
      direction: 0,
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
  enterPicture() {
    this.videoContext.showFloatingWindow(true);
  },
  exitPicture() {
    this.videoContext.exitPictureInPicture();
  }
});
```

特别的，tempFilePath ([本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)) 可以通过 [my.chooseVideo](https://opendocs.alipay.com/mini/api/media/video/my.choosevideo) 接口选取视频获得，例如：

```js
my.chooseVideo({
  sourceType: ['album', 'camera'],
  maxDuration: 30,
  camera: 'back',
  compressed: false,
  success: res => {
    // 该路径可用来播放视频
    const videoPath = res.tempFilePath;
    console.log(`videoPath = ${videoPath}`);
  },
});
```

## videoContext 方法列表

| **方法** | **参数** | **类型** | **描述** |
| --- | --- | --- | --- |
| play | 无 | - | 播放。 |
| pause | 无 | - | 暂停。 |
| stop | 无 | - | 停止。 |
| seek | position | Number | 跳转到指定位置，单位为秒（s）。 |
| requestFullScreen | direction | Number | 进入全屏。<br/><ul><li>0：正常竖屏。</li><li>90：横屏。</li><li>-90：反向横屏。</li></ul> |
| exitFullScreen | 无 | - | 退出全屏。 |
| showStatusBar | 无 | - | 显示状态栏，仅在 iOS 全屏下有效。 |
| hideStatusBar | 无 | - | 隐藏状态栏，仅在 iOS 全屏下有效。 |
| mute | ison | Boolean | 切换静音状态。 |
| playbackRate | rate | Number | 设置倍速播放（0.5 <= rate <= 2.0）。 |
| showFloatingWindow | isShow | Boolean | 显示/隐藏浮窗，例如 `showFloatingWindow(false)`。 |
| exitPictureInPicture | 无 | Function | 退出画中画。<br/> 基础库从 2.8.2 及以上版本支持，支付宝客户端版本从 10.1.92 开始支持。|


## video 组件的 onError 属性监听 错误码

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

## 常见问题 FAQ

### Q：怎么知道 videoContext 中方法是否调用成功？例如：我调用了 videoContext.play(), 怎么知道成功失败？
A：可以在 axml 文件中，通过 video 组件的 onError 属性监听视频播放是否出现了错误。

