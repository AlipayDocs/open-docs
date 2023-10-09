# 简介

**my.getBackgroundAudioManager** 是获取后台音频播放器的 API，与前景音频相对应，可以在用户离开当前小程序后继续播放音频。

更多信息，可查看 [音频播放 API 使用说明](https://opendocs.alipay.com/mini/03l3fn)。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

第一步：开发者可以在 .axml 文件中写入相关的组件来控制音乐的播放和暂停等，以下示例代码仅供参考：

```html
<!--.axml-->
<view>
  <button type="primary" onTap="audioPlay">开始播放背景音频</button>
</view>
<view>
  <button type="primary" onTap="audioPause">暂停播放背景音频</button>
</view>
<view>
  <button type="primary" onTap="audioStop">停止播放背景音频</button>
</view>
<view>
  <button type="primary" onTap="audioSeek">背景音频播放进度跳转</button>
</view>
```

第二步：获取背景音乐播放 backgroundAudioManager 后，添加属性并注册对应监听事件。

```javascript
//.js
onLoad(){
//获取背景音管理对象。
this.backgroundAudioManager = my.getBackgroundAudioManager();
//来源于优酷的音频码，默认为空字符串，当设置了新的 src 时，会自动开始播放。目前支持的格式有 m4a, aac, mp3, wav。如果开发者不传入音频码，控制台不会报错，但无音频播放。
this.backgroundAudioManager.src = '音频src';
//封面图 URL。用于做原生音频播放器背景图。原生音频播放器中的分享功能，分享的卡片配图及背景也将使用该图。
this.backgroundAudioManager.coverImgUrl = 'coverImgUrl';
//专辑名。原生音频播放器中的分享功能，分享出去的卡片简介，也将使用该值。
this.backgroundAudioManager.epname = 'epname';
//音频标题。用于做原生音频播放器音频标题。原生音频播放器中的分享功能，分享的卡片标题，也将使用该值。
this.backgroundAudioManager.title = 'title';
//歌手名。原生音频播放器中的分享功能，分享的卡片简介，也将使用该值。
this.backgroundAudioManager.singer = 'singer';
this.backgroundAudioManager.onPlay(()=>{
    console.log("backgroundAudioManager onPlay 开始播放")
    my.alert({ content:'backgroundAudioManager 背景音频播放事件 onPlay' });
});
this.backgroundAudioManager.onPause(()=>{
    console.log("backgroundAudioManager onPause 暂停播放")
    my.alert({ content:'backgroundAudioManager 背景音频暂停事件 onPause' });
});
this.backgroundAudioManager.onStop(()=>{
    console.log("backgroundAudioManager onStop")
    my.alert({ content:'backgroundAudioManager 背景音频停止事件 onStop' });
});
this.backgroundAudioManager.onSeeking(() => {
   console.log("backgroundAudioManageronSeeking 跳转播放事件")
   my.alert({ content:'backgroundAudioManager 背景音频跳转播放事件 onSeeking' });
});
this.backgroundAudioManager.onError((res)=>{
    console.log('backgroundAudioManager 背景音频播放错误事件 onError ')
    my.alert({ content: 'backgroundAudioManager 背景音频播放错误事件 onError' + JSON.stringify(res) });
});
},
```

第三步：开发者在 .js 文件中写入以下方法，配合上一步的组件，播放音频，以下示例代码仅供参考：

```javascript
//.js
audioPlay(){
    this.backgroundAudioManager.play();
    console.log("call backgroundAudioManager.play");
    my.alert({ content: "call backgroundAudioManager.play" });
  },
audioPause(){
    this.backgroundAudioManager.pause();
    console.log("call backgroundAudioManager.pause");
    my.alert({ content: "call backgroundAudioManager.pause" });
  },
audioStop(){
    this.backgroundAudioManager.stop();
    console.log("call backgroundAudioManager.stop");
    my.alert({ content: "call backgroundAudioManager.stop" });
  },
//播放进度调整
audioSeek(){
   this.backgroundAudioManager.seek(3.333);
   console.log("call backgroundAudioManager.seek");
   my.alert({ content: "backgroundAudioManager.seek" });
}
```

## 返回值

返回值为 backgroundAudioManager。

### backgroundAudioManager 属性列表

| **属性** | **类型** | **是否只读** | **描述** |
| --- | --- | --- | --- |
| duration | Number | 是 | 当前音频的长度，单位为秒（s），只有在当前有合法的 src 时返回。 |
| currentTime | Number | 是 | 当前音频的播放位置，单位为秒（s），只有在当前有合法的 src 时返回。 |
| paused | Boolean | 是 | 当前是是否暂停或停止状态，true 表示暂停或停止，false 表示正在播放。 |
| src | String | 否 | 音频码，默认为空字符串，当设置了新的 src 时，会自动开始播放 ，目前支持的格式有 m4a, AAC, MP3, WAV。如果开发者不传入音频码，控制台不会报错，但无音频播放。<br />**注意**：只支持来源于优酷的音频码。 |
| startTime | Number | 否 | 音频开始播放的位置，单位为秒（s）。默认从 0 开始播放。 |
| buffered | Number | 是 | 音频缓冲的时间点，仅保证当前播放时间点到此时间点内容已缓冲。 |
| title | String | 否 | 音频标题。原生音频播放器中的分享功能，分享出去的卡片标题，也将使用该值。 |
| epname | String | 否 | 专辑名。原生音频播放器中的分享功能，分享出去的卡片简介，也将使用该值。 |
| singer | String | 否 | 歌手名。原生音频播放器中的分享功能，分享的卡片简介，也将使用该值。 |
| coverImgUrl | String | 否 | 封面图 URL，用于做原生音频播放器背景图。原生音频播放器中的分享功能，分享的卡片配图及背景也将使用该图。以 URL 地址进行传参。 |
| webUrl | String | 否 | 页面链接，原生音频播放器中的分享功能，分享的卡片简介，也将使用该值。以 URL 地址进行传参。 |
| playbackRate | Number | 否 | 播放速度。范围 0.5-2.0，默认为 1。<br />**注意**：Android 需要 6 及以上版本支持。 |
| volume | Number | 否 | 音量。范围 0~1。例如：`this.backgroundAudioContext.volume = 0.5` |

### backgroundAudioManager 方法列表

| **方法** | **参数** | **描述** |
| --- | --- | --- |
| play | 无 | 播放。 |
| pause | 无 | 暂停。 |
| stop | 无 | 停止。 |
| seek | position | 跳转到指定位置，单位为秒（s）。精确到小数点后 3 位，即支持毫秒（ms）级别精确度。 |
| onCanplay | Function callback | 监听背景音频进入可以播放状态。但不保证后面可以流畅播放。 |
| onWaiting | Function callback | 监听音频加载中事件。当音频因为数据不足，需要停下来加载时会触发。 |
| onError | Function callback | 监听背景音频播放错误事件。 |
| onPlay | Function callback | 监听背景音频播放事件。 |
| onPause | Function callback | 监听背景音频暂停事件。 |
| onSeeking | Function callback | 监听背景音频开始播放进度跳转事件。 |
| onSeeked | Function callback | 监听背景音频完成播放进度跳转操作。 |
| onEnded | Function callback | 监听背景音频自然播放结束事件。 |
| onStop | Function callback | 监听背景音频停止事件。 |
| onTimeUpdate | Function callback | 监听背景音频播放进度更新事件。 |
| onNext | Function callback | 监听用户在系统音乐播放面板点击下一曲事件。 |
| onPrev | Function callback | 监听用户在系统音乐播放面板点击上一曲事件。 |

## 错误码

| **错误码** | **描述**   | **解决方案**             |
| ---------- | ---------- | ------------------------ |
| 10001      | 系统错误。 | 请检查手机系统，并重试。 |
| 10002      | 网络错误。 | 请检查网络设置，并重试。 |
| 10003      | 文件错误。 | 请检查文件，并重试。     |
| 10004      | 格式错误。 | 请检查格式问题，并重试。 |
| -1         | 未知错误。 | -                        |

# 常见问题 FAQ

## Q：进入页面播放音频，返回上一页后重新进入播放页面，为何 onTimeUpdate 等监听事件失效不执行？

A：onTimeUpdate 等监听事件在再次进入页面时失效不执行，二次进入界面的时候消息没办法传递出去，导致页面出错没有更新页面数据。

所以建议把之前的音频监听事件全部都 off 处理，然后再重新监听。

## Q：如何实现循环播放？

A：可以借助定时器或者 `onEnded()` 事件实现循环播放。

例如借助 `onEnded()` 事件实现循环播放：`onEnded()` 事件会在背景音频自然播放结束时触发，可在 `onEnded()` 方法中再次调用 `play()` 方法。
