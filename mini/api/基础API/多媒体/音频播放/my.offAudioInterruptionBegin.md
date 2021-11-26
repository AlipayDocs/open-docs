
# 简介
**my.offAudioInterruptionBegin** 是取消监听音频因为系统占用而被中断的开始事件。为异步接口。

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
//创建前景音上下文对象
this.innerAudioContext = my.createInnerAudioContext();
//来源于优酷的音频码，用于直接播放。支持音频格式：AAC，MP3。如果开发者不传入音频码，控制台不会报错，但无音频播放。
this.innerAudioContext.src = '音频src';
//是否自动开始播放，默认为 false
this.innerAudioContext.autoplay = false; 
//是否循环播放，默认为 false
this.innerAudioContext.loop = false;
//是否遵循系统静音开关，当此参数为 false 时，即使用户打开了静音开关，也能继续发出声音，默认值 true(注意：此参数仅 iOS 支持)。
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
//播放音乐
play() {
    this.innerAudioContext.play();
    console.log("call innerAudioContext.play");
    my.alert({ content: "call innerAudioContext.play" });
  },
//暂停播放
pause() {
    this.innerAudioContext.pause();
    console.log("call innerAudioContext.pause");
    my.alert({ content: "call innerAudioContext.pause" });
  },
//停止播放
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
//取消监听音频因为系统占用而被中断的开始事件
offAudioInterruptionBegin(){
  my.offAudioInterruptionBegin();
  console.log('innerAudioContext offAudioInterruptionBegin');
},
//取消监听音频被中断的结束事件
offAudioInterruptionEnd(){
  my.onAudioInterruptionEnd();
  console.log('innerAudioContext offAudioInterruptionEnd');
},
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| callback | Function | 音频因为受到系统占用而被中断的开始事件的回调函数。 |

