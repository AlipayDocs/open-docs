
# 简介
**my.createInnerAudioContext** 是在小程序内创建并返回内部音频（与背景音频相对应） innerAudioContext 对象的 API。又称“前景音频”，用户离开页面即停止播放。

更多信息，请参见 [音频播放](https://opendocs.alipay.com/mini/00d6hx)。

## 使用限制

- 基础库 [1.23.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.87 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 使用 **音频播放** 能力，请先在 [能力中心](https://nengli.alipay.com/abilityprod/detail?abilityCode=AM010501000000054210) 点击 **立即获取** 申请权限，否则将导致音频无法播放。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
第一步：开发者可以在 .axml 文件中写入相关的组件（如 button 或者 view）来控制音乐的播放和暂停等，以下示例代码仅供参考：
```html
<!--.axml-->
<view class="operation-item" onTap="play">播放</view>
<view class="operation-item" onTap="pause">暂停</view>
<view class="operation-item" onTap="stop">停止</view>
<view class="operation-item" onTap="seek">播放进度跳转</view>
<view class="operation-item" onTap="offAudioInterruptionBegin">取消监听音频因为系统占用而被中断的开始事件</view>
<view class="operation-item" onTap="offAudioInterruptionEnd">取消监听音频被中断的结束事件</view>
```
第二步：开发者获取前景音乐 innerAudioContext 对象后，添加属性并注册对应监听事件。
```javascript
//.js
onLoad(){
//创建前景音频上下文对象。
this.innerAudioContext = my.createInnerAudioContext(); 
//来源于优酷的音频码，用于直接播放。支持音频格式：AAC，MP3。如果开发者不传入音频码，控制台不会报错，但无音频播放。
this.innerAudioContext.src = '音频src'; 
//是否自动开始播放，默认为 false。
this.innerAudioContext.autoplay = false;
//是否循环播放，默认为 false。
this.innerAudioContext.loop = false;
//是否遵循系统静音开关，当此参数为 false 时，即使用户打开了静音开关，也能继续发出声音，默认值为 true (注意：此参数仅 iOS 支持)。
this.innerAudioContext.obeyMuteSwitch = false;
this.innerAudioContext.onPlay(() => {
   console.log("innerAudioContext onPlay 开始播放")
   my.alert({ content:'innerAudioContext 前景音频播放事件 onPlay' });
});
this.innerAudioContext.onPause(() => {
   console.log("innerAudioContext onPause 暂停播放")
   my.alert({ content:'innerAudioContext 前景音频暂停事件 onPause' });
});
this.innerAudioContext.onStop(() => {
   console.log("innerAudioContext onStop 停止播放")
   my.alert({ content:'innerAudioContext 前景音频停止事件 onStop' });
});
this.innerAudioContext.onSeeking(() => {
   console.log("innerAudioContext onSeeking 跳转播放事件")
   my.alert({ content:'innerAudioContext 前景音频跳转播放事件 onSeeking' });
});
this.innerAudioContext.onError(() => {
   console.log("innerAudioContext onError 前景音频播放错误事件")
   my.alert({ content:'innerAudioContext 前景音频播放错误事件 onError' });
});
//监听音频因为系统占用而被中断的开始事件
my.onAudioInterruptionBegin(() => {
  console.log('innerAudioContext onAudioInterruptionBegin');
});
//监听音频被中断的结束事件
my.onAudioInterruptionEnd(() => {
  console.log('innerAudioContext onAudioInterruptionEnd');
});
},
```
第三步：开发者在 .js 文件中写入以下方法，配合上一步的组件，播放音频，以下示例代码仅供参考：
```javascript
//.js
// 播放音乐
play() {
    this.innerAudioContext.play();
    console.log("call innerAudioContext.play");
    my.alert({ content: "call innerAudioContext.play" });
  },
// 暂停播放
pause() {
    this.innerAudioContext.pause();
    console.log("call innerAudioContext.pause");
    my.alert({ content: "call innerAudioContext.pause" });
  },
// 停止播放
stop() {
    this.innerAudioContext.stop()
    console.log("call innerAudioContext.stop");
    my.alert({ content: "call innerAudioContext.stop" });
  },
//播放进度调整
seek(){
   this.innerAudioContext.seek(3.333);
   console.log("call innerAudioContext.seek");
   my.alert({ content: "innerAudioContext.seek" });
},
//取消监听音频因为系统占用而被中断的开始事件。
offAudioInterruptionBegin(){
  my.offAudioInterruptionBegin();
  console.log('innerAudioContext offAudioInterruptionBegin');
},
//取消监听音频被中断的结束事件。
offAudioInterruptionEnd(){
  my.onAudioInterruptionEnd();
  console.log('innerAudioContext offAudioInterruptionEnd');
},
```

## 返回值
返回值为 innerAudioContext。

### innerAudioContext 属性列表
| **属性** | **类型** | **是否只读** | **说明** |
| --- | --- | --- | --- |
| src | String | 否 | 音频码，用于直接播放。支持音频格式：AAC，MP3。如果开发者不传入音频码，控制台不会报错，但无音频播放。                                  <br />**注意**：只支持来源于优酷的音频码。 |
| startTime | Number | 否 | 开始播放的位置，单位为秒（s），默认从 0 开始播放。 |
| autoplay | Boolean | 否 | 是否自动开始播放，默认为 false。 |
| loop | Boolean | 否 | 是否循环播放，默认为 false。 |
| obeyMuteSwitch | Boolean | 否 | 是否遵循系统静音开关，当此参数为 false 时，即使用户打开了静音开关，也能继续发出声音，默认值为 true。<br />**注意**：此参数仅 iOS 支持。 |
| duration | Number | 是 | 当前音频的长度，单位为秒（s），只有在当前有合法的 src 时返回。 |
| currentTime | Number | 是 | 当前音频的播放位置，单位为秒（s），只有在当前有合法的 src 时返回，时间不取整。 |
| paused | Boolean | 是 | 当前是否为暂停或停止状态，true 表示暂停或停止，false 表示正在播放。 |
| buffered | Number | 是 | 音频缓冲的时间点，仅保证当前播放时间点到此时间点内容已缓冲。 |
| volume | Number | 否 | 音量。范围 0~1。例如：`this.innerAudioContext.volump = 0.5` |
| playbackRate | Number | 否 | 播放速度。范围 0.5-2.0，默认为 1。<br />**注意**：Android 需要 6 及以上版本支持。 |


### innerAudioContext 方法列表
| **方法 ** | **参数** | **说明** |
| --- | --- | --- |
| play | 无 | 播放。 |
| pause | 无 | 暂停。 |
| stop | 无 | 停止。 |
| seek | position | 跳转到指定位置，单位为秒（s）。精确到小数点后 3 位，即支持 毫秒（ms） 级别精确度。 |
| destroy | 无 | 销毁当前实例。 |
| onCanplay | Function callback | 监听前景音频进入可以播放状态，但不保证后面可以流畅播放。 |
| onPlay | Function callback | 监听前景音频播放事件。 |
| onPause | Function callback | 监听前景音频暂停事件。 |
| onStop | Function callback | 监听前景音频停止事件。 |
| onEnded | Function callback | 监听前景音频自然播放结束事件。 |
| onTimeUpdate | Function callback | 监听前景音频播放进度更新事件。 |
| onError | Function callback | 监听前景音频播放错误事件。 |
| onWaiting | Function callback | 监听前景音频加载中事件，当音频因为数据不足，需要停下来加载时会触发。 |
| onSeeking | Function callback | 监听前景音频开始播放进度跳转的操作事件。 |
| onSeeked | Function callback | 监听前景音频完成播放进度跳转的操作事件。 |
| offCanplay | Function callback | 取消监听 onCanplay 事件。 |
| offPlay | Function callback | 取消监听 onPlay 事件。 |
| offPause | Function callback | 取消监听 onPause 事件。 |
| offStop | Function callback | 取消监听 onStop 事件。 |
| offEnded | Function callback | 取消监听 onEnded 事件。 |
| offTimeUpdate | Function callback | 取消监听 onTimeUpdate 事件。 |
| offError | Function callback | 取消监听 onError 事件。 |
| offWaiting | Function callback | 取消监听 onWaiting 事件。 |
| offSeeking | Function callback | 取消监听 onSeeking 事件。 |
| offSeeked | Function callback | 取消监听 onSeeked 事件。 |


## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 10001 | 系统错误。 | 请检查手机系统，并重试。 |
| 10002 | 网络错误。 | 请检查网络设置，并重试。 |
| 10003 | 文件错误。 | 请检查文件，并重试。 |
| 10004 | 格式错误。 | 请检查格式问题，并重试。 |
| -1 | 未知错误。 |  |


## 常见问题 FAQ

### Q：进入页面播放音频，返回上一页后重新进入播放页面，为何 onTimeUpdate 等监听事件失效不执行？
A：onTimeUpdate 等监听事件在再次进入页面时失效不执行，二次进入界面的时候消息没办法传递出去，导致页面出错没有更新页面数据。

所以建议把之前的音频监听事件全部都 off 处理，然后再重新监听。 
